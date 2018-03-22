---
layout: page
title: A day in the life of a bozo developer
description: What a common day in development looks like
---

**Disclaimer**: At every point in this process, I'm doing something
bozoriffic, and if you're a half-decent developer, you probably recognize
what it is. Yes, I'm an idiot and should learn my tools better. There,
I warned you.

### Bushy eyed and bright tailed...

So I've just finished watching Andrew Ng's wonderful lecture series
on convolutional nets, and I'm thinking _Hey, Facenet sounds like a good
solution to this problem I'm having!_ And, well, as long as I'm learning
ML, why not try to implement it myself?

Well, after a little while, I run into a confusing error in TensorFlow
(more on that later) and settle for a more tractable solution: why not
just find an existing implementation and use it?

Great, [here's](https://github.com/davidsandberg/facenet) a Python impl.
Should be pretty straightforward, right? Well, there are instructions on
how to _test_ it, but right now I want to train the thing. So I find the
most logical entrypoint, [train_tripletloss.py](https://github.com/davidsandberg/facenet/blob/master/src/train_tripletloss.py#L416),
only to discover that it takes 30 parameters:

{: style="overflow:scroll; height:300px;"}
```python
def parse_arguments(argv):
    parser = argparse.ArgumentParser()

    parser.add_argument('--logs_base_dir', type=str,
        help='Directory where to write event logs.', default='~/logs/facenet')
    parser.add_argument('--models_base_dir', type=str,
        help='Directory where to write trained models and checkpoints.', default='~/models/facenet')
    parser.add_argument('--gpu_memory_fraction', type=float,
        help='Upper bound on the amount of GPU memory that will be used by the process.', default=1.0)
    parser.add_argument('--pretrained_model', type=str,
        help='Load a pretrained model before training starts.')
    parser.add_argument('--data_dir', type=str,
        help='Path to the data directory containing aligned face patches.',
        default='~/datasets/casia/casia_maxpy_mtcnnalign_182_160')
    parser.add_argument('--model_def', type=str,
        help='Model definition. Points to a module containing the definition of the inference graph.', default='models.inception_resnet_v1')
    parser.add_argument('--max_nrof_epochs', type=int,
        help='Number of epochs to run.', default=500)
    parser.add_argument('--batch_size', type=int,
        help='Number of images to process in a batch.', default=90)
    parser.add_argument('--image_size', type=int,
        help='Image size (height, width) in pixels.', default=160)
    parser.add_argument('--people_per_batch', type=int,
        help='Number of people per batch.', default=45)
    parser.add_argument('--images_per_person', type=int,
        help='Number of images per person.', default=40)
    parser.add_argument('--epoch_size', type=int,
        help='Number of batches per epoch.', default=1000)
    parser.add_argument('--alpha', type=float,
        help='Positive to negative triplet distance margin.', default=0.2)
    parser.add_argument('--embedding_size', type=int,
        help='Dimensionality of the embedding.', default=128)
    parser.add_argument('--random_crop',
        help='Performs random cropping of training images. If false, the center image_size pixels from the training images are used. ' +
         'If the size of the images in the data directory is equal to image_size no cropping is performed', action='store_true')
    parser.add_argument('--random_flip',
        help='Performs random horizontal flipping of training images.', action='store_true')
    parser.add_argument('--keep_probability', type=float,
        help='Keep probability of dropout for the fully connected layer(s).', default=1.0)
    parser.add_argument('--weight_decay', type=float,
        help='L2 weight regularization.', default=0.0)
    parser.add_argument('--optimizer', type=str, choices=['ADAGRAD', 'ADADELTA', 'ADAM', 'RMSPROP', 'MOM'],
        help='The optimization algorithm to use', default='ADAGRAD')
    parser.add_argument('--learning_rate', type=float,
        help='Initial learning rate. If set to a negative value a learning rate ' +
        'schedule can be specified in the file "learning_rate_schedule.txt"', default=0.1)
    parser.add_argument('--learning_rate_decay_epochs', type=int,
        help='Number of epochs between learning rate decay.', default=100)
    parser.add_argument('--learning_rate_decay_factor', type=float,
        help='Learning rate decay factor.', default=1.0)
    parser.add_argument('--moving_average_decay', type=float,
        help='Exponential decay for tracking of training parameters.', default=0.9999)
    parser.add_argument('--seed', type=int,
        help='Random seed.', default=666)
    parser.add_argument('--learning_rate_schedule_file', type=str,
        help='File containing the learning rate schedule that is used when learning_rate is set to to -1.', default='data/learning_rate_schedule.txt')

    # Parameters for validation on LFW
    parser.add_argument('--lfw_pairs', type=str,
        help='The file containing the pairs to use for validation.', default='data/pairs.txt')
    parser.add_argument('--lfw_file_ext', type=str,
        help='The file extension for the LFW dataset.', default='png', choices=['jpg', 'png'])
    parser.add_argument('--lfw_dir', type=str,
        help='Path to the data directory containing aligned face patches.', default='')
    parser.add_argument('--lfw_nrof_folds', type=int,
        help='Number of folds to use for cross validation. Mainly used for testing.', default=10)
    return parser.parse_args(argv)
```
<small>
(Sheepish note: the repo *does* have good instructions on how to use it. I just 
missed them.)
</small>

Okay, do I try to figure this out, or... hey, there's [this sweet node.js wrapper](https://github.com/zixia/node-facenet)
that makes it easy as one click! I just have to run a `demo.ts`.

Now, not having any frontend skillz, I only vaguely recognize `.ts` as
something called TypeScript. Some quick Googling suggests that I can
run it with something called `ts-node`, which I hastily install. And so begins...

## My short-lived career in TypeScript
```
$ ts-node demo.ts

...

ImportError: This package should not be accessible on Python 3. Either you are trying to run from the python-future src folder or your installation of python-future is corrupted.
…
```

Uh, what? We'll come back to this later, but some more quick Googling
(noticing a pattern here?) suggests I've mangled my `PYTHONPATH`. So now:

```
$ unset PYTHONPATH

$ ts-node demo.ts
...
/usr/local/lib/node_modules/ts-node/src/index.ts:307
        throw new TSError(formatDiagnostics(diagnosticList, cwd, ts, lineOffset))
              ^

TSError: ⨯ Unable to compile TypeScript
demo.ts (19,26): Cannot find name '__dirname'. (2304)
```

Dangit, what? I find [three](https://github.com/TypeStrong/ts-node/issues/271)
[github](https://github.com/electron/electron-typescript-definitions/issues/43)
[issues](https://github.com/mgechev/angular-seed/issues/147), none of
which I really understand, and some of which point me down further rabbit
holes. How much time should I spend figuring this out? I don't think anything
went wrong with my `npm install`, but just to be safe....

```
$ npm install
…
/bin/sh: pkg-config: command not found
…
```

Some "quick Googling" (tm) and:
```
$ brew install zeromq
$ brew install pkgconfig
$ npm install
…
No package 'pixman-1' found
…

$ brew install pixman
$ npm install
…
No package 'cairo' found
…

$ brew install cairo
$ npm install
…
No package 'pangocairo' found
…

$ brew install pangocairo
…
Error: No available formula with the name "pangocairo"
…

$ brew install pango
(success)
```

Sure, each step required more Googling to figure out the relevant package,
but I'm _getting closer!_ I can feel it now!

```
$ npm install
dyld: Library not loaded: /usr/local/opt/icu4c/lib/libicui18n.58.dylib
  Referenced from: /usr/local/bin/node
  Reason: image not found
zsh: trace trap  npm install
```

**W.T.F., mate?** Is it time to bail yet? No, someone has an
[answer](https://github.com/Homebrew/homebrew-core/issues/11713)!
```
$ brew reinstall node --without-icu4c
==> Reinstalling node --without-icu4c
==> Downloading https://nodejs.org/dist/v8.9.1/node-v8.9.1.tar.xz

######################################################################## 100.0%

==> ./configure --prefix=/usr/local/Cellar/node/8.9.1 --without-npm
==> make install

… 30 min later, fan spinning …
```

Time to clock out of the salt mines. When I come back the next day:
```
$ npm install
… success!!! …
```

_Sweet Jesus, yes!_ Now let's give this puppy a whirl!
```
$ ts-node demo.ts

Error: error while reading from input stream
    at Image.src (/Users/aditpras/git/node-facenet/node_modules/canvas/lib/image.js:30:17)
    at Promise (/Users/aditpras/git/node-facenet/node_modules/canvas/index.js:34:15)
    at new Promise (<anonymous>)
    at loadImage (/Users/aditpras/git/node-facenet/node_modules/canvas/index.js:23:10)
    at Object.<anonymous> (/Users/aditpras/git/node-facenet/src/misc.ts:108:23)
    at Generator.next (<anonymous>)
    at /Users/aditpras/git/node-facenet/src/misc.ts:7:71
    at new Promise (<anonymous>)
    at __awaiter (/Users/aditpras/git/node-facenet/src/misc.ts:3:12)
    at Object.loadImage (/Users/aditpras/git/node-facenet/src/misc.ts:103:12)
    at Facenet.<anonymous> (/Users/aditpras/git/node-facenet/src/facenet.ts:138:27)
    at Generator.next (<anonymous>)
    at /Users/aditpras/git/node-facenet/src/facenet.ts:7:71
    at new Promise (<anonymous>)
    at __awaiter (/Users/aditpras/git/node-facenet/src/facenet.ts:3:12)
    at Facenet.align (/Users/aditpras/git/node-facenet/src/facenet.ts:118:16)
```

Ack! Bad puppy! Luckily, it tells me exactly which line (118) to debug:

{: style="overflow:scroll; height:300px;"}
```typescript
     98   /**
     99    *
    100    * Do face alignment for the image, return a list of faces.
    101    * @param {(ImageData | string)} imageData
    102    * @returns {Promise<Face[]>} - a list of faces
    103    * @example
    104    * const imageFile = `${__dirname}/../tests/fixtures/two-faces.jpg`
    105    * const faceList = await facenet.align(imageFile)
    106    * console.log(faceList)
    107    * // Output
    108    * // [ Face {
    109    * //     id: 0,
    110    * //     imageData: ImageData { data: [Object] },
    111    * //     confidence: 0.9999634027481079,
    112    * //     landmark:
    113    * //      { leftEye: [Object],
    114    * //        rightEye: [Object],
    115    * //        nose: [Object],
    116    * //        leftMouthCorner: [Object],
    117    * //        rightMouthCorner: [Object] },
    118    * //      location: { x: 360, y: 94, w: 230, h: 230 },
    119    * //      md5: '003c926dd9d2368a86e41a2938aacc98' },
    120    * //   Face {
    121    * //     id: 1,
    122    * //     imageData: ImageData { data: [Object] },
    123    * //     confidence: 0.9998626708984375,
    124    * //     landmark:
    125    * //      { leftEye: [Object],
    126    * //        rightEye: [Object],
    127    * //        nose: [Object],
    128    * //        leftMouthCorner: [Object],
    129    * //        rightMouthCorner: [Object] },
    130    * //     location: { x: 141, y: 87, w: 253, h: 253 },
    131    * //     md5: '0451a0737dd9e4315a21594c38bce485' } ]
```

That's right, `facenet.ts:118` is a _comment_. Typescript is wackier than
I thought.

You know what? Maybe I really am better off trying to resolve my
TensorFlow problems.


## Python

Okay, well, my team is using Python 3 and I've been using 2. Shouldn't
be a problem to have them work together on my Mac, right?

```
$ python3

Failed to import the site module

Traceback (most recent call last):
  File "/usr/local/lib/python2.7/site-packages/site.py", line 73, in <module>
    __boot()
…
    raise ImportError('This package should not be accessible on Python 3. '

ImportError: This package should not be accessible on Python 3. Either you are trying to run from the python-future src folder or your installation of python-future is corrupted.
```

Wait, why is `python3` trying to access something from `python2.7`?
Well, when you install Python 2 with homebrew, `pip install` puts stuff in a
location that's not in the `sys.path` of the system Python at
`/usr/bin/python`. That's okay, though, because homebrew's Python is in
`/usr/local/opt/python/libexec/bin`, which is on your `PATH`, and its
`sys.path` is correct.

Nonetheless, you sometimes come across something that invokes the
system Python so
[a common solution](https://stackoverflow.com/questions/25276329/cant-load-python-modules-installed-via-pip-from-site-packages-directory)
is to add to your `PYTHONPATH` in one of your login scripts:

```
export PYTHONPATH=$PYTHONPATH:/usr/local/lib/python2.7/site-packages
```

So far so good. Except when you try to run Python 3, of course, when you get
the error we see above. Perhaps that "common solution" isn't so nice after
all. So you remove that from your `PYTHONPATH`, and now Python 3 works.

But `pip3` still doesn't.
```
$ pip3 install tensorflow

Traceback (most recent call last):
  File "/usr/local/bin/pip3", line 5, in <module>
    from pkg_resources import load_entry_point
  File "/Library/Python/2.7/site-packages/pkg_resources/__init__.py", line 74, in <module>
    import appdirs

ImportError: No module named appdirs
```

Of course, you can't just `pip3 install` appdirs, because you can't `pip3`
for some reason, because it's still referencing a `python2.7` path.

Confused yet?

Relax, take a deep breath, and reason through this with me.

```
$ cat `which pip3`

#!/usr/bin/python
...
```

A ha, got you, you [milky bastard](https://www.youtube.com/watch?v=__Mwvp3vsC0)!
That's the _system_ `python2.7`! I bet for some reason we're not using
Homebrew's `pip3`, even though we installed `python3`.

So now we look up "homebrew install pip3", and get a
[straightforward answer](https://stackoverflow.com/questions/34573159/how-do-install-pip3-on-my-mac/47004414#47004414)
Homebrew needs some extra lovin' to get `python3` and `pip3` working:

```
$ brew upgrade python3

==> Upgrading 1 outdated package, with result:
python3 3.6.4_2

==> Upgrading python3
Error: Permission denied @ unlink_internal - /usr/local/bin/2to3-3.6
```

I swear this looks familiar. Oh, right, for some reason I have to periodically do
```
$ sudo chown -R "$USER":admin /usr/local
```

Now we're cooking!
```
$ brew upgrade python3
...(success)...

$ brew postinstall python3
...(success)...

$ pip3 install tensorflow

Traceback (most recent call last):
  File "/usr/local/bin/pip3", line 5, in <module>
    from pkg_resources import load_entry_point
  File "/Library/Python/2.7/site-packages/pkg_resources/__init__.py", line 74, in <module>
    import appdirs

ImportError: No module named appdirs
```

Dude, what? Well, if you'd just been _paying attention_, you'd have
discovered [this comment](https://stackoverflow.com/questions/34573159/how-do-install-pip3-on-my-mac#comment68972880_34574269)
buried in the thread:

  * _For some reason it didn't work. anw, put in .profile: pip3='python3 -m pip'_

**TADA!** Tensorflow installed!

Should be smooth sailing from here!

<small>
Leaving aside that while debugging I removed
`/usr/local/opt/python/libexec/bin` from my `PATH` and forgot to put it back,
trapping me in a spin cycle of misery....
Also, lest you think that was actually the *end* of my Python woes, consider
that I never actually fixed the fact that anything trying to access
the system python2.7 will [still fail](more-python.html).
</small>

## Wrangling TensorFlow

Let's not get into the weeds of what I'm trying to do here. There's
more detail [here](keras-tf-pyfunc.html)
if you're interested. The point is that when you're trying to build a
TensorFlow-based model, and you need to execute arbitrary Python code
in the middle (i.e., something that does not do pure tensor manipulation),
you can use something called `tf.py_func` to invoke it.

Or at least, you think you can. This code takes the *indices* of some
pictures in `x_train` as input, and returns the images.

```python
  def fetch_img(x_train):
    def _fetch_img(x):
      return tf.py_func(lambda x: x_train[x.flatten()],
                        [x], tf.float32)
    return _fetch_img

  inp = Input(shape=(1,), dtype=tf.uint16)
  fetched_imgs = Lambda(fetch_img(x_train))(inp)
```

When you try to test this code in a simplified model, running `predict`
without training it, it works:

```python
  model = Model(inp, fetched_imgs)

  indices = np.array([1, 5, 10])

  actual = model.predict(indices)
  expected = x_train[x_in]
  assert np.array_equal(actual, expected)
```

And yet, when you try to `compile` the model, you get this sweet error:
```
Traceback (most recent call last):
  File "my_model.py", line 35, in <module>
    optimizer=keras.optimizers.Adam(lr=1e-5))
  File "/Users/ml/Library/Python/2.7/lib/python/site-packages/keras/engine/training.py", line 742, in compile
    target = K.placeholder(ndim=len(shape),
TypeError: object of type 'NoneType' has no len()
```

Unfortunately, no StackOverflow or Github Issues to the rescue here.
So you roll up your sleeves and dig into the TensorFlow codebase. The
problem is that you forgot to explicitly set the shape of the tensor
returned in `_fetch_img()`. Which is _obvious_-- how was TF going to know
the dimensions of your output? You didn't need to trawl through a
foreign codebase to figure that out, right?
```python
   def _fetch_img(x):
     res = tf.py_func(lambda x: x_train[x.flatten()], [x], tf.float32)
     res.set_shape((x.shape[0],) + x_train[0].shape)
     return res
```

Cool. Finally, everything works! Unfortunately, when you try to train it
(with `fit`), more fun awaits....

{: style="overflow:scroll; height:300px;"}
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

What went wrong?

Well how do you think TensorFlow is going to back-propagate
the gradients through your layer, when you haven't defined its derivative
(gradient) function, dummy?
It's clearly telling you that you must [define a custom gradient](https://stackoverflow.com/questions/41535347/how-gradient-passed-by-tf-py-func):

```python
# Define custom py_func which takes also a grad op as argument:
def py_func(func, inp, Tout, stateful=True, name=None, grad=None):

    # Need to generate a unique name to avoid duplicates:
    rnd_name = 'PyFuncGrad' + str(np.random.randint(0, 1E+8))

    tf.RegisterGradient(rnd_name)(grad)  # see _MySquareGrad for grad example
    g = tf.get_default_graph()
    with g.gradient_override_map({"PyFunc": rnd_name}):
        return tf.py_func(func, inp, Tout, stateful=stateful, name=name)
```

But let's leave all this aside for now. Because by this point, all I'm
interested in is sharing with the world how much fun development can be.
But Blogger sucks. What are the cool kids using these days?


## github.io

I've seen people make sweet sites on [github.io](https://pages.github.com/).
How hard can it be? First, you create a github repo named `monkstatic.github.io`, and then
you uh... install some software that can make web...sites?

Right-o, at least they recommend one: [jekyll](https://jekyllrb.com/),
"Transform your plain text into static websites and blogs." Sweet, so it's
like... Apache? Nope. It requires knowing stuff. Do I want to take the plunge?

Luckily, I stumble onto this (genuinely awesome)
[tutorial](http://kbroman.org/simple_site/) that walks me through it step by step.

First step is to clone his repo, but his example doesn't use the
`[username].github.io` naming convention. Will it still be hosted on
that domain? Do I have to connect them somehow? Should I carefully read
the official documentation or plow ahead with my experimentation and worry
about it later? How much effort will it be to undo my mistakes this time?

I choose to plow ahead. (For the record, on something like page four of
the official doc, it does explain how repos other than the one named
`username.github.io` can still be hosted there. But I doubt I could have made
sense of the doc without getting my hands dirty. As so often, chicken and egg.)

While going through the tutorial, I realize I've checked in my IntelliJ's
`.idea` folder, which is a no-no. But do _you_ remember how to remove it
from your git _index_ without nuking your _working copy_? If you said
`git rm -r --cached`, you're right, but if you said "computers are obnoxious"
you're even more right.

Instead, I stumble down a dark alley (having forgotten that there
_is no_ `master` branch in this repo), and by the time I remember to
run `git rm` with the proper flags, it instead invokes Cthulhu, forcing
me to start over lest he feast on my increasingly tender brain.

I emerge worn but victorious. I make a note to get back my `git`-fu.

Anyway, I finish the tutorial, and it works! Except, _dangit_, there's
no syntax highlighting in the code blocks. But not to fear! Jekyll's documentation explains
that the Rouge syntax highlighter will take care of things for me! The thing
is, it's already the default. So is my `_config.yaml` wrong? How about
my use of ["kramdown"](https://kramdown.gettalong.org/)?

I don't know, but you bet I'm gonna find out!

### Gotta rougify your kramdown, son

I figure maybe it's worth slowing down and reading some documentation
for a change. So I locate [Rouge's official demo site](http://rouge.jayferd.us/demo).
When I click that, it redirects to admarketplace.com, which redirects somewhere
else, and eventually dumps me out at Edmunds.com. Because I wanted to
buy a car. I try again, and it dumps me on clickvalidator.net, which
informs me that my clicks are suspicious. I agree, it is pretty suspicious that
I'm still trying to get this to work when I could go outside and smell some
roses or something similarly monktastic.

Okay, try again. This SO answer to
["Jekyll not highlighting with rouge highlighter"](https://stackoverflow.com/a/37773310/5175433)
looks promising! But hmm, it claims that
```
Another thing, if you want to "color your code", you need an highlight css.
```

That doesn't sound like _another_ thing, that sounds like _the_ thing!
How do I get _that_? By typing "rouge highlight css" into
Google and crossing my fingers, of course. Whaddya know,
there's [a hit](https://benhur07b.github.io/2017/03/25/add-syntax-highlighting-to-your-jekyll-site-with-rouge.html)!

Thus begins...

### My short-lived career in Ruby

Step one:
```
$ gem install kramdown rouge
Fetching: kramdown-1.16.2.gem (100%)
ERROR:  While executing gem ... (Gem::FilePermissionError)
    You don't have write permissions for the /Library/Ruby/Gems/2.0.0 directory.
```

Maybe `sudo chown` to the rescue? Nah, don't be a bozo. There must be a good 
reason for this. [You see](https://stackoverflow.com/a/14607772/5175433),

_"That is the version of Ruby installed by Apple, for their own use."_

That's funny, I could have sworn I bought this computer _from_ Apple.
Anyway, I have (at least) a few options:

1. Get your own damn Ruby! (i.e., `brew install ruby`)
2. Use a sledgehammer (i.e., use `sudo`)
3. Use a Ruby version manager (like `rbenv`)
4. "Try" adding `--user-install`

Each approach has its champions and detractors, but the fourth is the
[most up-voted](https://stackoverflow.com/a/38259128/5175433). Plus,
the comments say that it is "simple and logical," two of my favorite things!

  * _This is simple and logical. Add ruby path if you haven't in your bashrc_:
``` bash
if which ruby >/dev/null && which gem >/dev/null; then
    PATH="$(ruby -rubygems -e 'puts Gem.user_dir')/bin:$PATH"
fi
```

Did I accidentally eat LSD or did he? It turns out neither; it comes from the
[official Ruby doc](http://guides.rubygems.org/faqs/#user-install). Now all
I have to do is make sure it works with `zsh`. Not like there could be [subtle
but obnoxious differences](http://slopjong.de/2012/07/02/compatibility-between-zsh-and-bash/) that could bite me in
the behind. That *never* happens.

I nope out of there real fast and settle on the trusty `homebrew`.

```
$ brew install ruby
... stuff ...

$ gem install kramdown rouge --user-install
WARNING:  You don't have /Users/aditpras/.gem/ruby/2.0.0/bin in your PATH, gem executables will not run.
… other good stuff …
```

Okay fine, I'll add `/Users/aditpras/.gem/ruby/2.0.0/bin` to my `PATH`.
But oops, I forgot to install `jekyll`:
```
$ gem install jekyll --user-install
WARNING:  You don't have /Users/aditpras/.gem/ruby/2.5.0/bin in your PATH, gem executables will not run.
...
```

_What?!_ Where did `2.5.0` suddenly come from? No matter, I still need
to `rougify` with some `monokai`. No time to waste! I still have
somewhere between zero and infinity steps left after this one!

```
$ rougify style monokai > assets/css/syntax.css
```

Are we there yet? I don't know... is the Python code in this document
colored?

I sure hope so, because there's something I was trying to get done. Now
if only I could remember what it was....