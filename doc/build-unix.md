Copyright (c) 2009-2013 Bitcoin Developers

Distributed under the MIT/X11 software license, see the accompanying
file COPYING or http://www.opensource.org/licenses/mit-license.php.
This product includes software developed by the OpenSSL Project for use in the [OpenSSL Toolkit](http://www.openssl.org/). This product includes
cryptographic software written by Eric Young ([eay@cryptsoft.com](mailto:eay@cryptsoft.com)), and UPnP software written by Thomas Bernard.

UNIX BUILD NOTES
====================

To Build
---------------------

	cd src/
	make -f makefile.unix		# Headless Bells

See readme-qt.rst for instructions on building Bells-Qt, the graphical user interface.

Dependencies
---------------------

 Library     Purpose           Description
 -------     -------           -----------
 libssl      SSL Support       Secure communications
 libdb4.8    Berkeley DB       Blockchain & wallet storage
 libboost    Boost             C++ Library
 miniupnpc   UPnP Support      Optional firewall-jumping support

Berkeley DB 4.8 is required. Newer versions change the wallet file format and
must not be used. OpenSSL 1.1 and 3.x are not supported: the 0.8.x sources use
the OpenSSL 1.0 API (opaque BIGNUM/ECDSA/EVP structures, `BN_init`,
`EVP_CIPHER_CTX_init`). Use OpenSSL 1.0.2u.

[miniupnpc](http://miniupnp.free.fr/) may be used for UPnP port mapping.  It can be downloaded from [here](
http://miniupnp.tuxfamily.org/files/).  UPnP support is compiled in and
turned off by default.  Set USE_UPNP to a different value to control this:

	USE_UPNP=     No UPnP support miniupnp not required
	USE_UPNP=0    (the default) UPnP support turned off by default at runtime
	USE_UPNP=1    UPnP support turned on by default at runtime

IPv6 support may be disabled by setting:

	USE_IPV6=0    Disable IPv6 support

Licenses of statically linked libraries:
 Berkeley DB   New BSD license with additional requirement that linked
               software must be free open source
 Boost         MIT-like license
 miniupnpc     New (3-clause) BSD license

Versions known to work with this tree:

-  GCC           13.2 (C++11 or later required)
-  OpenSSL       1.0.2u
-  Berkeley DB   4.8.30.NC
-  Boost         1.83.0
-  Qt            5.15 (graphical wallet only)
-  miniupnpc     1.6 or newer

Boost 1.73 and later no longer declare the `boost::bind` placeholders (`_1`,
`_2`) in the global namespace. This tree already includes the compatibility
fix, so no manual changes are required.

Dependency Build Instructions: Ubuntu & Debian
----------------------------------------------
Build requirements:

	sudo apt-get install build-essential
	sudo apt-get install libssl-dev

Most current distributions ship OpenSSL 3.x and Berkeley DB 5.x, which are not
compatible with this code base. Build OpenSSL 1.0.2u and Berkeley DB 4.8.30
from source (see below) and point the build at them with `OPENSSL_INCLUDE_PATH`,
`OPENSSL_LIB_PATH`, `BDB_INCLUDE_PATH` and `BDB_LIB_PATH`.

Optional:

	sudo apt-get install libminiupnpc-dev (see USE_UPNP compile flag)


Notes
-----
The release is built with GCC and then "strip bellsd" to strip the debug
symbols, which reduces the executable size by about 90%.


miniupnpc
---------
	tar -xzvf miniupnpc-1.6.tar.gz
	cd miniupnpc-1.6
	make
	sudo make install


Berkeley DB
-----------
You need Berkeley DB 4.8.  If you have to build Berkeley DB yourself:

	cd build_unix
	../dist/configure --enable-cxx --disable-shared --prefix=/usr/local
	make
	sudo make install


OpenSSL
-------
OpenSSL 1.0.2u has to be built separately:

	./config no-shared -fcommon --prefix=/usr/local/ssl-1.0.2
	make
	sudo make install_sw

`-fcommon` is required with GCC 10 and later.


Boost
-----
If you need to build Boost yourself:

	./bootstrap.sh
	./b2 --layout=system link=static threading=multi cxxstd=11 install

Security
--------
To help make your Bells installation more secure by making certain attacks impossible to
exploit even if a vulnerability is found, you can take the following measures:

* Position Independent Executable
    Build position independent code to take advantage of Address Space Layout Randomization
    offered by some kernels. An attacker who is able to cause execution of code at an arbitrary
    memory location is thwarted if he doesn't know where anything useful is located.
    The stack and heap are randomly located by default but this allows the code section to be
    randomly located as well.

    On an Amd64 processor where a library was not compiled with -fPIC, this will cause an error
    such as: "relocation R_X86_64_32 against `......' can not be used when making a shared object;"

    To build with PIE, use:
    make -f makefile.unix ... -e PIE=1

    To test that you have built PIE executable, install scanelf, part of paxutils, and use:

    	scanelf -e ./Bells

    The output should contain:
     TYPE
    ET_DYN

* Non-executable Stack
    If the stack is executable then trivial stack based buffer overflow exploits are possible if
    vulnerable buffers are found. By default, bitcoin should be built with a non-executable stack
    but if one of the libraries it uses asks for an executable stack or someone makes a mistake
    and uses a compiler extension which requires an executable stack, it will silently build an
    executable without the non-executable stack protection.

    To verify that the stack is non-executable after compiling use:
    `scanelf -e ./Bells`

    the output should contain:
	STK/REL/PTL
	RW- R-- RW-

    The STK RW- means that the stack is readable and writeable but not executable.
