---
layout: page
title: Making an independent website
description: How to make an independent website with GitHub Pages.
---

### A Keras layer that loads images by index

Say you have a Keras model that processes images in your training set,
stored in numpy array `x_train`. Suppose you want it to instead take
as input the _indices_ of the images, rather than the images themselves.
This can be useful if, for example, you want to store those indices at
a later stage. What might that code look like?

First, your input (the index) is a scalar, but [Keras doesn't let you
use scalar inputs](https://github.com/keras-team/keras/issues/2776).
Easiest might be to make it have shape `(1,)`:

```python
 inp = Input(shape=(1,))
```

Next, you might try to use a `Lambda` layer to extract the image from the input:
```python
 def fetch_img(x):
   return x_train[x.flatten()]

 fetch_img = Lambda(fetch_img)(inp)
```

If `x = [[1], [2], [3]]` (i.e., a bunch of arrays of shape `(1,)`), then
we want to turn it into `[1, 2, 3]`, so we `flatten it`. Recall that
`x_train[[1, 2, 3]]` is the same as `x_train[[1, 2, 3], : , : , : ]`,
which selects images 1, 2, and 3.

Next, we don't want to hardcode the use of `x_train`:
```python
 def fetch_img(x_train):
   def _fetch_img(x):
     return x_train[x.flatten()]
   return _fetch_img

 fetched_imgs = Lambda(fetch_img(x_train))(inp)
```

But we still have a problem: `x` is of type `Tensor`, and the function
given to `Lambda` must also return a `Tensor`. We're trying to operate
on a numpy array (`x_train`).

Often the function you see passed to Lambda will appear to be a
mathematical operation:
```python
Lambda(lambda x: x + 4)
```

but that's really an overloaded TF op (e.g., `tf.Tensor.__add__(x, y)`).
If you want to run arbitrary Python code, you have to invoke
[tf.py_func](https://www.tensorflow.org/api_docs/python/tf/py_func):
```python
 def fetch_img(x_train):
   def _fetch_img(x):
     return tf.py_func(lambda x: x_train[x.flatten()],
                       [x], tf.float32)
   return _fetch_img
```

Seems like it works! The following `assert` passes:
```python
  def fetch_img(x_train):
    def _fetch_img(x):
      return tf.py_func(lambda x: x_train[x.flatten()],
                        [x], tf.float32)
   return _fetch_img

  inp = Input(shape=(1,), dtype=tf.uint16)
  fetched_imgs = Lambda(fetch_img(x_train))(inp)
  model = Model(inp, fetched_imgs)

  x_in = np.array([1, 5, 10])
  res = model.predict(x_in)
  exp = x_train[x_in]
  assert np.array_equal(res, exp)
```


So now you carry on, building up your model, until it comes time to
compile it:
```python
model.compile(
    loss=keras.losses.mae,
    optimizer=keras.optimizers.Adam(lr=1e-5))
```

But _bam_:
```
Traceback (most recent call last):
  File "my_model.py", line 35, in <module>
    optimizer=keras.optimizers.Adam(lr=1e-5))
  File "/Users/ml/Library/Python/2.7/lib/python/site-packages/keras/engine/training.py", line 742, in compile
    target = K.placeholder(ndim=len(shape),
TypeError: object of type 'NoneType' has no len()
```

Good luck sorting that one out. Turns out you have to explicitly set the shape:
```python
 def fetch_img(x_train):
   def _fetch_img(x):
     res = tf.py_func(lambda x: x_train[x.flatten()], [x], tf.float32)
     res.set_shape((x.shape[0],) + x_train[0].shape)
     return res
   return _fetch_img
```

Cool! Everything works!

Since this is the first layer in your model, Keras doesn't need to
calculate gradients to pass back to previous layers. But what if you
have a `tf.py_func` that comes later?

Well, then, it will compile, but when you try to `fit` it:
```python
model.fit(x_train, y_train)
```

You get this sweet stack trace:
```
---------------------------------------------------------------------------
ValueError                                Traceback (most recent call last)
<ipython-input-21-4c5e910353fd> in <module>()
      5     optimizer=keras.optimizers.Adam(lr=1e-5))
      6
----> 7 facenet.fit(x_train, y_train)

/home/ml/.local/lib/python2.7/site-packages/keras/engine/training.pyc in fit(self, x, y, batch_size, epochs, verbose, callbacks, validation_split, validation_data, shuffle, class_weight, sample_weight, initial_epoch, steps_per_epoch, validation_steps, **kwargs)
   1575         else:
   1576             ins = x + y + sample_weights
-> 1577         self._make_train_function()
   1578         f = self.train_function
   1579

/home/ml/.local/lib/python2.7/site-packages/keras/engine/training.pyc in _make_train_function(self)
    958                     training_updates = self.optimizer.get_updates(
    959                         params=self._collected_trainable_weights,
--> 960                         loss=self.total_loss)
    961                 updates = self.updates + training_updates
    962                 # Gets loss and metrics. Updates weights at each call.

/home/ml/.local/lib/python2.7/site-packages/keras/legacy/interfaces.pyc in wrapper(*args, **kwargs)
     85                 warnings.warn('Update your `' + object_name +
     86                               '` call to the Keras 2 API: ' + signature, stacklevel=2)
---> 87             return func(*args, **kwargs)
     88         wrapper._original_function = func
     89         return wrapper

/home/ml/.local/lib/python2.7/site-packages/keras/optimizers.pyc in get_updates(self, loss, params)
    430
    431         for p, g, m, v in zip(params, grads, ms, vs):
--> 432             m_t = (self.beta_1 * m) + (1. - self.beta_1) * g
    433             v_t = (self.beta_2 * v) + (1. - self.beta_2) * K.square(g)
    434             p_t = p - lr_t * m_t / (K.sqrt(v_t) + self.epsilon)

/home/ml/.local/lib/python2.7/site-packages/tensorflow/python/ops/math_ops.pyc in binary_op_wrapper(x, y)
    883       if not isinstance(y, sparse_tensor.SparseTensor):
    884         try:
--> 885           y = ops.convert_to_tensor(y, dtype=x.dtype.base_dtype, name="y")
    886         except TypeError:
    887           # If the RHS is not a tensor, it might be a tensor aware object

/home/ml/.local/lib/python2.7/site-packages/tensorflow/python/framework/ops.pyc in convert_to_tensor(value, dtype, name, preferred_dtype)
    834       name=name,
    835       preferred_dtype=preferred_dtype,
--> 836       as_ref=False)
    837
    838

/home/ml/.local/lib/python2.7/site-packages/tensorflow/python/framework/ops.pyc in internal_convert_to_tensor(value, dtype, name, as_ref, preferred_dtype, ctx)
    924
    925     if ret is None:
--> 926       ret = conversion_func(value, dtype=dtype, name=name, as_ref=as_ref)
    927
    928     if ret is NotImplemented:

/home/ml/.local/lib/python2.7/site-packages/tensorflow/python/framework/constant_op.pyc in _constant_tensor_conversion_function(v, dtype, name, as_ref)
    227                                          as_ref=False):
    228   _ = as_ref
--> 229   return constant(v, dtype=dtype, name=name)
    230
    231

/home/ml/.local/lib/python2.7/site-packages/tensorflow/python/framework/constant_op.pyc in constant(value, dtype, shape, name, verify_shape)
    206   tensor_value.tensor.CopyFrom(
    207       tensor_util.make_tensor_proto(
--> 208           value, dtype=dtype, shape=shape, verify_shape=verify_shape))
    209   dtype_value = attr_value_pb2.AttrValue(type=tensor_value.tensor.dtype)
    210   const_tensor = g.create_op(

/home/ml/.local/lib/python2.7/site-packages/tensorflow/python/framework/tensor_util.pyc in make_tensor_proto(values, dtype, shape, verify_shape)
    369   else:
    370     if values is None:
--> 371       raise ValueError("None values not supported.")
    372     # if dtype is provided, forces numpy array to be the type
    373     # provided if possible.

ValueError: None values not supported.
```

The problem (_obviously_) is that Keras doesn't know how to backpropagate
through this layer.