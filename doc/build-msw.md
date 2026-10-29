WINDOWS BUILD NOTES
===================

This document describes how the Bells 0.8.7.1 Windows binaries are produced.
The verified procedure is a cross-compile from Linux with MinGW-w64, for both
64-bit (x86_64) and 32-bit (i686) targets.

The graphical wallet (`bells-qt.exe`) is built with Qt 5.15.2; the daemon
(`bellsd.exe`) needs no Qt. Both executables are statically linked against
Boost, Berkeley DB, OpenSSL and LevelDB, so the only runtime dependencies are
the Windows system DLLs, the MinGW runtime and (for the wallet) the Qt DLLs.

Copyright (c) 2009-2013 Bitcoin Developers
Distributed under the MIT/X11 software license, see the accompanying
file COPYING or http://www.opensource.org/licenses/mit-license.php.


1. Host requirements
--------------------

Any recent x86_64 Linux distribution works. On Debian/Ubuntu:

    sudo apt-get install build-essential autoconf libtool pkg-config \
        perl python3 rsync unzip wget

A MinGW-w64 toolchain with both targets and POSIX threads is required. The
release binaries were built with GCC 13.2; the Ubuntu packages provide the
same compiler:

    sudo apt-get install g++-mingw-w64-x86-64-posix g++-mingw-w64-i686-posix

This installs `x86_64-w64-mingw32-g++` and `i686-w64-mingw32-g++`.

All commands below assume a scratch directory and two installation prefixes,
one per architecture, so that 32-bit and 64-bit libraries never mix:

    export WORK=$HOME/bells-winbuild
    mkdir -p $WORK
    PREFIX64=$WORK/prefix64
    PREFIX32=$WORK/prefix32


2. Berkeley DB 4.8.30.NC
------------------------

Wallet files are Berkeley DB 4.8 databases. Newer versions change the file
format and cannot read an existing `wallet.dat`, so 4.8.30 is mandatory.

Download `db-4.8.30.NC.tar.gz` from Oracle, then for each architecture:

    tar xzf db-4.8.30.NC.tar.gz
    cd db-4.8.30.NC
    mkdir build_win64 && cd build_win64
    ../dist/configure --host=x86_64-w64-mingw32 --build=x86_64-pc-linux-gnu \
        --enable-mingw --enable-cxx --disable-shared --disable-replication \
        --prefix=$PREFIX64
    make -j$(nproc)
    make install

Repeat in a separate copy of the tree with `--host=i686-w64-mingw32` and
`--prefix=$PREFIX32`. Do not reuse the build directory between architectures.

This installs `libdb_cxx.a` and the headers into the prefix. Only the C++
library is needed.


3. Boost 1.83.0
---------------

Boost is used for filesystem, threading, program options, signals and Asio.
Build it statically for both targets. Create a `user-config.jam` per target:

    using gcc : win64 : x86_64-w64-mingw32-g++
        : <archiver>x86_64-w64-mingw32-ar <ranlib>x86_64-w64-mingw32-ranlib ;

    using gcc : win32 : i686-w64-mingw32-g++
        : <archiver>i686-w64-mingw32-ar <ranlib>i686-w64-mingw32-ranlib ;

Then, from the Boost source directory:

    ./bootstrap.sh
    ./b2 -j$(nproc) --user-config=$WORK/user-config-win64.jam \
        toolset=gcc-win64 target-os=windows architecture=x86 address-model=64 \
        link=static runtime-link=static threading=multi variant=release \
        cxxstd=11 --layout=system \
        --prefix=$PREFIX64 \
        --with-system --with-filesystem --with-program_options \
        --with-thread --with-chrono --with-date_time --with-atomic \
        install

Repeat with the 32-bit toolset, `address-model=32` and `$PREFIX32`.

`--layout=system` produces unsuffixed names (`libboost_thread.a`), which is why
`BOOST_LIB_SUFFIX` is empty in the project file. `cxxstd=11` is required: the
0.8.x sources use `std::unique_ptr` and C++11 features.

Boost 1.83 removed the global `boost::bind` placeholders (`_1`, `_2`). The tree
already contains the fix (`#include <boost/bind.hpp>` in the two Qt models and
`BOOST_BIND_GLOBAL_PLACEHOLDERS` in the project file), so no manual patching is
needed.


4. OpenSSL 1.0.2u
-----------------

The 0.8.x sources use the OpenSSL 1.0 API directly (opaque BIGNUM/ECDSA/EVP
structures, `BN_init`, `EVP_CIPHER_CTX_init`, `SSLeay_version`). OpenSSL 1.1
and 3.x will not compile or link. Use 1.0.2u:

    wget https://www.openssl.org/source/openssl-1.0.2u.tar.gz
    tar xzf openssl-1.0.2u.tar.gz

64-bit:

    cp -a openssl-1.0.2u openssl-win64 && cd openssl-win64
    CROSS_COMPILE=x86_64-w64-mingw32- ./Configure mingw64 \
        no-shared no-asm -fcommon --prefix=$WORK/openssl64
    make -j$(nproc)
    make install_sw

32-bit:

    cp -a openssl-1.0.2u openssl-win32 && cd openssl-win32
    CROSS_COMPILE=i686-w64-mingw32- ./Configure mingw \
        no-shared no-asm -fcommon --prefix=$WORK/openssl32
    make -j$(nproc)
    make install_sw

`-fcommon` avoids multiple-definition errors caused by GCC 10 and later
defaulting to `-fno-common`.


5. LevelDB
----------

LevelDB is bundled in `src/leveldb` and is built as part of the tree. To build
it manually (required once before linking, and as a pre-target dependency of
the qmake project):

    cd src/leveldb
    chmod +x build_detect_platform
    TARGET_OS=OS_WINDOWS_CROSSCOMPILE make -j$(nproc) \
        CC=x86_64-w64-mingw32-gcc CXX=x86_64-w64-mingw32-g++ \
        OPT="-O2 -w -std=gnu++11" libleveldb.a libmemenv.a
    x86_64-w64-mingw32-ranlib libleveldb.a libmemenv.a

Use the i686 toolchain for the 32-bit build. Build each architecture in its own
copy of the source tree, since the archives are not interchangeable.

Note: the source path must not contain spaces. `lrelease` and the LevelDB
makefile both break on paths with spaces, so copy the tree to a plain path
before building the wallet.


6. Daemon (bellsd.exe)
----------------------

The historical `src/makefile.linux-mingw` can be used, but it expects
`boost_*-mt-s` library names. With the Boost build above
(`--layout=system`) either set

    BOOST_LIB_SUFFIX=  LDFLAGS="-static"  CXX=x86_64-w64-mingw32-g++

or compile directly. The essential flags are:

    DEFS="-D_MT -DWIN32 -D_WINDOWS -DBOOST_THREAD_USE_LIB \
          -DBOOST_SPIRIT_THREADSAFE -DUSE_IPV6=1 -DHAVE_BUILD_INFO"

    x86_64-w64-mingw32-g++ -c -std=gnu++11 -O2 \
        $DEFS \
        -I. -Ijson -Iqt -Iobj \
        -Ileveldb/include -Ileveldb/helpers \
        -I$WORK/openssl64/include -I$PREFIX64/include \
        -o obj/<name>.o <name>.cpp

and link with:

    x86_64-w64-mingw32-g++ -std=gnu++11 -O2 \
        -Wl,--dynamicbase -Wl,--nxcompat -static \
        -o bellsd.exe obj/*.o \
        leveldb/libleveldb.a leveldb/libmemenv.a \
        -L$WORK/openssl64/lib -L$PREFIX64/lib \
        -lboost_system -lboost_filesystem -lboost_program_options \
        -lboost_thread -lboost_chrono \
        -ldb_cxx -lssl -lcrypto \
        -lws2_32 -lmswsock -lshlwapi -lole32 -loleaut32 -luuid -lgdi32 \
        -lcomdlg32 -lwinspool -lwinmm -lshell32 -lcomctl32 -ladvapi32 \
        -lrpcrt4 -liphlpapi -lcrypt32 -luserenv -lwsock32

`-static` links the MinGW runtime (including `libwinpthread`) into the
executable, so `bellsd.exe` only needs the Windows system DLLs.

The `-L` order matters: the OpenSSL directory must come before the prefix that
also contains Boost, otherwise the linker may pick a wrong `libcrypto`.

For 32-bit, replace the toolchain prefix, use `address-model=32` libraries and
add `-Wl,--large-address-aware`.


7. Qt wallet (bells-qt.exe)
---------------------------

Qt 5.15.2 MinGW binaries are published by the Qt project:

* `qtbase-Windows-Windows_7-Mingw-Windows-Windows_7-X86_64.7z` (64-bit)
* `qtbase-Windows-Windows_7-Mingw-Windows-Windows_7-X86.7z` (32-bit)

Only the `qtbase` archive is needed (Core, Gui, Widgets, Network and the
`qwindows` platform plugin). Extract it, for example, to
`$WORK/qt64/5.15.2/mingw81_64` and `$WORK/qt32/5.15.2/mingw81_32`.

The wallet is built with qmake. Use the `win32-g++` mkspec of the extracted Qt
installation and override the compiler tools, because qmake itself runs on the
host:

    qmake -early \
        "QMAKE_CXX=x86_64-w64-mingw32-g++" \
        "QMAKE_CC=x86_64-w64-mingw32-gcc" \
        "QMAKE_LINK=x86_64-w64-mingw32-g++" \
        "QMAKE_LINK_C=x86_64-w64-mingw32-gcc" \
        "QMAKE_AR=x86_64-w64-mingw32-ar cqs" \
        "QMAKE_RANLIB=x86_64-w64-mingw32-ranlib" \
        "QMAKE_RC=x86_64-w64-mingw32-windres" \
        "QMAKE_STRIP=x86_64-w64-mingw32-strip" \
        bitcoin-qt.pro -spec win32-g++ \
        "RELEASE=1" "USE_UPNP=-" "MINGW_THREAD_BUGFIX=0" \
        "USE_BUILD_INFO=1" "USE_QRCODE=0" \
        "BOOST_LIB_SUFFIX=" "BOOST_THREAD_LIB_SUFFIX=" "BDB_LIB_SUFFIX=" \
        "BOOST_INCLUDE_PATH=$PREFIX64/include" \
        "BOOST_LIB_PATH=$PREFIX64/lib" \
        "BDB_INCLUDE_PATH=$PREFIX64/include" \
        "BDB_LIB_PATH=$PREFIX64/lib" \
        "OPENSSL_INCLUDE_PATH=$WORK/openssl64/include" \
        "OPENSSL_LIB_PATH=$WORK/openssl64/lib"

    make -j$(nproc)

For the 32-bit build run the same command in a separate build directory,
replacing the toolchain prefix with `i686-w64-mingw32-`, pointing the paths to
`$PREFIX32` / `$WORK/openssl32`, and adding `"LAA=1"` to enable the
large-address-aware linker flag (the i686 linker supports it, the x86_64 linker
does not).

The resulting executable is `release/Bells-qt.exe`.

### Notes and known pitfalls

* `bitcoin-qt.pro` already contains the Qt 5 / Boost 1.83 compatibility
  changes: `-std=gnu++11`, empty `BOOST_LIB_SUFFIX`,
  `BOOST_BIND_GLOBAL_PLACEHOLDERS`, additional system libraries for the
  statically linked OpenSSL, and the architecture dependent
  `--large-address-aware` flag.
* `QMAKE_LIBS_OPENGL` is taken from the Windows mkspec; no override is needed
  when the Qt mkspecs come from the extracted Qt installation.
* `lrelease` runs as part of qmake. If the project path contains spaces, the
  translation step fails with "cannot open ... .qm"; build from a path without
  spaces.
* Do not put the OpenSSL 1.1 or 3.x headers into a directory that is also on
  the include path of Boost/Berkeley DB. `#include <openssl/bn.h>` would
  resolve to the wrong version and the build would fail with
  `invalid use of incomplete type 'BIGNUM'`.


8. Deployment
-------------

Create a directory containing:

    bellsd.exe
    bells-qt.exe
    Qt5Core.dll  Qt5Gui.dll  Qt5Widgets.dll  Qt5Network.dll
    libwinpthread-1.dll
    libstdc++-6.dll
    libgcc_s_seh-1.dll   (64-bit)  /  libgcc_s_dw2-1.dll  (32-bit)
    platforms/qwindows.dll
    imageformats/qgif.dll  imageformats/qico.dll  imageformats/qjpeg.dll
    styles/qwindowsvistastyle.dll

The Qt DLLs and plugins come from the Qt installation; the MinGW runtime DLLs
come from the compiler toolchain and must match the architecture. The
executables are statically linked against everything else.

Qt locates its plugins relative to the executable, so the `platforms`
directory must stay next to `bells-qt.exe`. Distribute the whole directory as
a ZIP archive; no installer is required.


9. Verifying the result
-----------------------

    file bellsd.exe bells-qt.exe
    x86_64-w64-mingw32-objdump -p bellsd.exe | grep "DLL Name"

The daemon should import only system DLLs (`KERNEL32.dll`, `WS2_32.dll`,
`ADVAPI32.dll`, ...), and the wallet should add `Qt5Core.dll`, `Qt5Gui.dll`,
`Qt5Widgets.dll`, `Qt5Network.dll` and `libwinpthread-1.dll`.
