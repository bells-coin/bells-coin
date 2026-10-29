Bells-Qt: Qt 5 GUI for Bells
============================

Build instructions
==================

The graphical wallet is built from `bitcoin-qt.pro` with qmake. It requires the
same libraries as the daemon (Boost, Berkeley DB 4.8, OpenSSL 1.0.2) plus Qt 5.

Full platform notes:

* Windows (native or cross-compile): `doc/build-msw.md`
* Linux: `doc/build-unix.md`
* macOS: `doc/build-osx.md`

Debian / Ubuntu
---------------

Install the build tools and the Qt 5 development packages:

::

    apt-get install build-essential pkg-config git

    apt-get install qtbase5-dev qttools5-dev-tools \
        libboost-dev libboost-system-dev libboost-filesystem-dev \
        libboost-program-options-dev libboost-thread-dev

Berkeley DB 4.8 and OpenSSL 1.0.2 are usually not packaged by current
distributions. Build them from source as described in `doc/build-unix.md` and
pass their locations to qmake:

::

    qmake \
        BOOST_INCLUDE_PATH=/usr/local/include \
        BOOST_LIB_PATH=/usr/local/lib \
        BDB_INCLUDE_PATH=/usr/local/db48/include \
        BDB_LIB_PATH=/usr/local/db48/lib \
        OPENSSL_INCLUDE_PATH=/usr/local/ssl-1.0.2/include \
        OPENSSL_LIB_PATH=/usr/local/ssl-1.0.2/lib \
        BOOST_LIB_SUFFIX= BDB_LIB_SUFFIX=
    make

An executable named `Bells-Qt` is created in the current directory.

Alternatively, open `bitcoin-qt.pro` in Qt Creator and build as usual.

Common qmake options:

::

    RELEASE=1          link the runtime libraries statically where possible
    USE_UPNP=          build without UPnP support
    USE_QRCODE=1       enable the QR code dialog (needs libqrencode)
    USE_IPV6=0         disable IPv6
    BOOST_LIB_SUFFIX=  suffix for the Boost library names, empty for
                       --layout=system builds (default: -mgw44-mt-s-1_50
                       on Windows)

Mac OS X
--------

- Download and install the `Qt Mac OS X SDK`_. It is recommended to also install
  Apple's Xcode with the command line tools.

- Install dependencies with `HomeBrew`_:

::

    brew install boost miniupnpc openssl berkeley-db4

- Edit `bitcoin-qt.pro` or pass the library locations to qmake to account for
  Homebrew paths, then build with qmake or Qt Creator.

.. _`Qt Mac OS X SDK`: http://qt-project.org/downloads/
.. _`HomeBrew`: http://mxcl.github.io/homebrew/
