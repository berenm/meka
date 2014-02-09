===============================================
Meka: C++11 meta make prototype.
===============================================
.. image:: https://secure.travis-ci.org/berenm/meka.png?branch=master
    :alt: Build Status
    :target: https://travis-ci.org/berenm/meka


USAGE
````````````````````````````
Meka allows you to describe the build process of your projects using C++.
A ``meka`` file at the root of the project contains the description of the project and the target to build.

Meka itself is described this way, and can build itself, once a precursor is available or bootstraped.

Calling ``meka`` binary will trigger the compilation of the ``meka`` descriptor into another ``meka`` binary that
will embed knowlegde of the project build process. This new ``meka`` will then run and compile the rest of the
project.

.. code:: cpp

  #include <meka.hpp>

  extern meka::package meka;
  extern meka::package boost;

  meka::package foo = {
    path    = meka::this_dir(),
    name    = "foo",
    version = "0.0.1",

    meka::lib {
      name     = "bar",
      sources  = { "src/.*\\.cpp" },
      links    = { "boost_filesystem" },
    },

    meka::bin {
      name    = "bla",
      sources = { "src/main.cpp", "src/test.cpp" },
    },
  };


BUILD
````````````````````````````
Meka currently uses Ninja for dependency managment. The goal is not to rely on some external make program, and this should be internalized.
However Ninja is also required for bootstraping Meka, when no precursor is available. Ninja sources are linked as a submodule, in bin/ninja.

.. code:: bash

  ninja
  ./build/meka


COPYING INFORMATION
````````````````````````````

 Distributed under the Boost Software License, Version 1.0.

 See accompanying file LICENSE or copy at http://www.boost.org/LICENSE_1_0.txt


.. image:: https://d2weczhvl823v0.cloudfront.net/berenm/meka/trend.png
   :alt: Bitdeli badge
   :target: https://bitdeli.com/free

