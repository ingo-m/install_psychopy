# MovieStim in Psychopy

*Work in progress, problem not solved yet.*

An attempt at creating a manual installation of psychopy in order to get
movie stimuli with sound to work. (On Debian and/or Mac.)

The goal is to get stimuli such as the following sample to work:
```
python ~/psychopy/demos/coder/stimuli/MovieStim.py
```

* On Mac, install Xcode (manually)

* Create a new virtual environment for this endeavour:
  ```
  conda create -n py_psychopy
  ```

* Install a lot of dependencies:
  ```
  pip install numpy scipy

  pip install matplotlib pandas pyopengl pyglet pillow moviepy lxml openpyxl xlrd configobj pyyaml gevent greenlet msgpack-python psutil tables requests[security] pyosf cffi pysoundcard pysoundfile seaborn psychopy_ext python-bidi psychopy

  pip install pyserial pyparallel egi iolabs

  pip install pytest coverage sphinx

  pip install pyobjc

  pip install pygame

  conda install -c anaconda wxpython

  conda install -c anaconda pyaudio

  conda install -c anaconda gcc

  conda install -c conda-forge libsndfile
  ```

  `cd` into directory where you whish to install psychopy and clone Psychopy
  repository, e.g.:
  ```
  cd /home/john/GitHub/
  git clone https://github.com/psychopy/psychopy.git
  pip install -e ~/psychopy
  ```

* go into python, import `imageio` and install `ffmpeg`, and exit python:
  ```
  python
  import imageio
  imageio.plugins.ffmpeg.download()
  exit()
  ```

* Restart terminal, go into virtual environment again:
  ```
  source activate py_psychopy
  ```

* Install `pyo` - this does not work
  ```
  cd /home/john/GitHub/
  git clone https://github.com/belangeo/pyo.git
  pip install -e /home/john/GitHub/pyo
  ```
  Output:
  ```
  pip install -e /Users/john/1_PhD/GitHub/pyo
  Obtaining file:///Users/john/1_PhD/GitHub/pyo
  Installing collected packages: pyo
    Running setup.py develop for pyo
      Complete output from command /Users/john/miniconda2/envs/py_psychopy/bin/python -c "import setuptools, tokenize;__file__='/Users/john/1_PhD/GitHub/pyo/setup.py';f=getattr(tokenize, 'open', open)(__file__);code=f.read().replace('\r\n', '\n');f.close();exec(compile(code, __file__, 'exec'))" develop --no-deps:
      running develop
      running egg_info
      writing pyo.egg-info/PKG-INFO
      writing top-level names to pyo.egg-info/top_level.txt
      writing dependency_links to pyo.egg-info/dependency_links.txt
      warning: manifest_maker: standard file '-c' not found

      reading manifest file 'pyo.egg-info/SOURCES.txt'
      writing manifest file 'pyo.egg-info/SOURCES.txt'
      running build_ext
      building '_pyo' extension
      gcc -fno-strict-aliasing -I/Users/john/miniconda2/envs/py_psychopy/include -arch x86_64 -DNDEBUG -g -fwrapv -O3 -Wall -Wstrict-prototypes -DUSE_PORTAUDIO -DUSE_PORTMIDI -DUSE_OSC -D_OSX_ -Iinclude -I/usr/local/include -I/opt/local/include -I/Users/john/miniconda2/envs/py_psychopy/include/python2.7 -c src/engine/pyomodule.c -o build/temp.macosx-10.7-x86_64-2.7/src/engine/pyomodule.o -Wno-strict-prototypes -Wno-strict-aliasing -O3 -g0
      In file included from src/engine/pyomodule.c:34:0:
      include/ad_portaudio.h:25:23: fatal error: portaudio.h: No such file or directory
       #include "portaudio.h"
                             ^
      compilation terminated.
      error: command 'gcc' failed with exit status 1

      ----------------------------------------
  Command "/Users/john/miniconda2/envs/py_psychopy/bin/python -c "import setuptools, tokenize;__file__='/Users/john/1_PhD/GitHub/pyo/setup.py';f=getattr(tokenize, 'open', open)(__file__);code=f.read().replace('\r\n', '\n');f.close();exec(compile(code, __file__, 'exec'))" develop --no-deps" failed with error code 1 in /Users/john/1_PhD/GitHub/pyo/
  ```

...

* Installing `pyo` manually from the website
  www.ajaxsoundstudio.com/software/pyo/ does not help because the system-wide
  installation does cannot be imported within the virtual environment.

  After installing `pyo` system-wide using the installer provided on the
  website, it is available in system (root) python, but cannot be imported:
  ```
  which python
  /usr/bin/python
  johns-mbp:~ john$ python
  Python 2.7.10 (default, Feb  6 2017, 23:53:20)
  [GCC 4.2.1 Compatible Apple LLVM 8.0.0 (clang-800.0.34)] on darwin
  Type "help", "copyright", "credits" or "license" for more information.
  >>> import pyo
  Traceback (most recent call last):
    File "<stdin>", line 1, in <module>
    File "/Library/Python/2.7/site-packages/pyo.py", line 21, in <module>
      import pyolib.analysis as analysis
    File "/Library/Python/2.7/site-packages/pyolib/analysis.py", line 32, in <module>
      from ._core import *
    File "/Library/Python/2.7/site-packages/pyolib/_core.py", line 57, in <module>
      from _pyo import *
  ImportError: dlopen(/Library/Python/2.7/site-packages/_pyo.so, 2): Library not loaded: /usr/local/opt/flac/lib/libFLAC.8.dylib
    Referenced from: /usr/local/lib/libsndfile.1.dylib
    Reason: image not found
  ```

  The virtual environment does not see `pyo`:
  ```
  which python
  /Users/john/miniconda2/bin/python
  johns-mbp:~ john$ python
  Python 2.7.12 |Continuum Analytics, Inc.| (default, Jul  2 2016, 17:43:17)
  [GCC 4.2.1 (Based on Apple Inc. build 5658) (LLVM build 2336.11.00)] on darwin
  Type "help", "copyright", "credits" or "license" for more information.
  Anaconda is brought to you by Continuum Analytics.
  Please check out: http://continuum.io/thanks and https://anaconda.org
  >>> import pyo
  Traceback (most recent call last):
    File "<stdin>", line 1, in <module>
  ImportError: No module named pyo
  ```
