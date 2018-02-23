
Some weeks later....

```
$ aubiocut
Traceback (most recent call last):
  File "/usr/local/Cellar/aubio/0.4.6/libexec/bin/aubiocut", line 6, in <module>
    from pkg_resources import load_entry_point
  File "/Library/Python/2.7/site-packages/pkg_resources/__init__.py", line 74, in <module>
    import appdirs
ImportError: No module named appdirs
```

I'm gonna lose it. What about:

```
$ PYTHONPATH=$PYTHONPATH:/usr/local/lib/python2.7/site-packages aubiocut
…
ImportError: No module named appdirs
```

Because:
```
$ head -3 `which aubiocut`
#!/bin/bash
PYTHONPATH="" exec "/usr/local/Cellar/aubio/0.4.6/libexec/bin/aubiocut" "$@"
```

Okay, what if we install appdirs using the pip accessible to `/usr/bin/python`?
```
$ /usr/bin/python -m pip install appdirs
/usr/bin/python: No module named appdirs; 'pip' is a package and cannot be directly executed
```

Supposedly that indicates an old version of pip. So:
```
$ sudo /usr/bin/easy_install pip
Password:
Traceback (most recent call last):
  File "/usr/bin/easy_install-2.7", line 7, in <module>
    from pkg_resources import load_entry_point
  File "/Library/Python/2.7/site-packages/pkg_resources/__init__.py", line 74, in <module>
    import appdirs
ImportError: No module named appdirs
```

Okay what if I manually install appdirs?
```
$ wget https://pypi.python.org/packages/48/69/d87c60746b393309ca30761f8e2b49473d43450b150cb08f3c6df5c11be5/appdirs-1.4.3.tar.gz#md5=44c679904082a2133f5566c8a0d3ab42

$ tar zxvf appdirs-1.4.3.tar.gz
$ cd appdirs-1.4.3
$ chmod a+x setup.py
$ ./setup.py install
Copying appdirs-1.4.3-py2.7.egg to /usr/local/lib/python2.7/site-packages
```

D'oh! That's the `site-packages` of brew's python.
```
$ head -2 setup.py
#!/usr/bin/env python
```

A ha! Change that to: `#!/usr/bin/python`. Now:
```
$ ./setup.py install
Copying appdirs-1.4.3-py2.7.egg to /Library/Python/2.7/site-packages
```

Still doesn't work. F*** it. I'll fold and create a virtualenv.

Now, when pip installing aubio:
```
  In file included from python/ext/aubiomodule.c:2:
  python/ext/aubio-types.h:16:10: fatal error: 'numpy/arrayobject.h' file not found
  #include <numpy/arrayobject.h>
           ^
  1 error generated.
  error: command 'cc' failed with exit status 1
```

Looks like only brew install is supported, and brew doesn't respect virtualenv. Okay let's fix the above error:

```
$ export CFLAGS="-I /usr/local/lib/python2.7/site-packages/numpy/core/include $CFLAGS"
```

...

