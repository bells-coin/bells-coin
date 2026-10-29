Bells (BEL)
===========

Bells is a peer-to-peer electronic cash system forked from Litecoin, using
scrypt as its proof-of-work algorithm and DigiShield for per-block difficulty
retargeting. This repository contains the Bells 0.8.7.1 reference client:
`bellsd` (headless daemon) and `bells-qt` (graphical wallet).

    Website:  http://www.bellscoin.org
    Symbol:   BEL
    License:  MIT (see COPYING)

Project status
--------------

Bells 0.8.7.1 is the final release of the 0.8.x codebase (2014). It is a
legacy codebase and is no longer under active development, but it is kept
buildable so that old wallets and block chain data remain accessible.

The tree has been updated to compile with a current toolchain:

| Component        | Version used for the Windows release builds |
|------------------|---------------------------------------------|
| Compiler         | GCC 13.2 (MinGW-w64, x86_64 and i686)        |
| Boost            | 1.83.0                                       |
| Berkeley DB      | 4.8.30.NC                                    |
| OpenSSL          | 1.0.2u                                       |
| LevelDB          | bundled in `src/leveldb`                     |
| Qt               | 5.15.2 (MinGW builds)                        |

Source compatibility patches for Boost 1.83 / Qt 5 / modern MinGW are included
in this repository. See [doc/build-msw.md](doc/build-msw.md) for the exact
Windows build procedure.

Prebuilt Windows binaries are available on the
[releases page](https://github.com/bells-coin/bells-coin/releases):

* `bells-0.8.7.1-win64.zip` - 64-bit build (x86_64)
* `bells-0.8.7.1-win32.zip` - 32-bit build (i686)

Translations
------------

This description and the installation instructions are also available in other
languages. See the [translation index](doc/i18n/README.md) or open a language
directly:

[العربية](doc/i18n/README.ar.md) ·
[বাংলা](doc/i18n/README.bn.md) ·
[Български](doc/i18n/README.bg.md) ·
[简体中文](doc/i18n/README.zh.md) ·
[Suomi](doc/i18n/README.fi.md) ·
[Français](doc/i18n/README.fr.md) ·
[Deutsch](doc/i18n/README.de.md) ·
[हिन्दी](doc/i18n/README.hi.md) ·
[Magyar](doc/i18n/README.hu.md) ·
[Bahasa Indonesia](doc/i18n/README.id.md) ·
[Italiano](doc/i18n/README.it.md) ·
[日本語](doc/i18n/README.ja.md) ·
[한국어](doc/i18n/README.ko.md) ·
[Polski](doc/i18n/README.pl.md) ·
[Português](doc/i18n/README.pt.md) ·
[Русский](doc/i18n/README.ru.md) ·
[Español](doc/i18n/README.es.md) ·
[Türkçe](doc/i18n/README.tr.md) ·
[اردو](doc/i18n/README.ur.md)

The English text is the reference; translations may lag behind after an update.

Coin specification
------------------

| Parameter                  | Value                                        |
|----------------------------|----------------------------------------------|
| Proof of work              | scrypt                                       |
| Block target time          | 2.5 minutes                                  |
| Difficulty retargeting     | every block (DigiShield)                     |
| Total supply               | 500,000,000 BEL                              |
| P2P port (mainnet)         | 19919                                        |
| RPC port (mainnet)         | 19918                                        |
| P2P port (testnet)         | 29919                                        |
| RPC port (testnet)         | 29918                                        |
| Address prefix             | `B`                                          |
| Protocol version           | 70002                                        |
| Data directory (Windows)   | `%APPDATA%\Bells`                            |
| Data directory (Unix)      | `~/.bells`                                   |
| Configuration file         | `bells.conf`                                 |

Block rewards
-------------

Each block pays one of the following rewards, selected at random:

| Probability | Reward        |
|-------------|---------------|
| 50%         | 50 BEL        |
| 20%         | 100 BEL       |
| 14%         | 250 BEL       |
| 10%         | 500 BEL       |
| 5%          | 1,000 BEL     |
| 1%          | 10,000 BEL    |

The schedule changes at the following heights:

* block 129,600 (~90 days): reward halved
* block 259,200 (~180 days): reduced to 4/5
* block 518,400 (~1 year): fixed reward of 2 BEL

Getting started (Windows)
-------------------------

1. Download and unpack the archive for your architecture. Keep all files and
   subdirectories together; the executables will not start without the bundled
   Qt libraries and the `platforms` directory.
2. Run `bells-qt.exe` for the graphical wallet, or `bellsd.exe` for the daemon.
3. On first start the client creates its data directory and `wallet.dat`:

       %APPDATA%\Bells

   Back up `wallet.dat` before using the wallet with real funds.

Portable mode is available with `-datadir=<path>` (for example
`bells-qt.exe -datadir=D:\BellsData`).

### Running the daemon

    bellsd.exe                  run in the current console (Ctrl+C to stop)
    bellsd.exe --help           list all command line options
    bellsd.exe getinfo          example RPC call

Windows does not support Unix-style daemonization, so `-daemon` has no effect.
Use `start /b bellsd.exe` to run the daemon without a separate console window.

### Configuration

Settings are read from `%APPDATA%\Bells\bells.conf` (or `-conf=<file>`). A
minimal server configuration:

    server=1
    rpcuser=username
    rpcpassword=change-me
    rpcallowip=127.0.0.1
    rpcport=19918
    port=19919
    # addnode=1.2.3.4:19919
    # listen=1
    # upnp=0

The daemon and the GUI can share the same data directory, but only one process
may open the wallet at a time.

### Common command line options

| Option             | Description                                          |
|--------------------|------------------------------------------------------|
| `-datadir=<dir>`   | Use an alternative data directory                    |
| `-conf=<file>`     | Use an alternative configuration file                |
| `-testnet`         | Connect to the test network                          |
| `-connect=<host>`  | Connect only to the given node                       |
| `-listen=0`        | Do not accept incoming connections                   |
| `-rpcuser` / `-rpcpassword` | RPC credentials                            |
| `-rpcallowip=<ip>` | Allow RPC connections from the given address         |
| `-gen=0`           | Disable mining (mining is off by default)            |

A full list is printed by `bellsd.exe --help`.

Building from source
--------------------

The build produces two targets:

* `src/bellsd` (or `bellsd.exe` on Windows) - headless daemon
* `bells-qt` (or `bells-qt.exe` on Windows) - Qt wallet, built from
  `bitcoin-qt.pro`

Detailed platform notes:

* [doc/build-msw.md](doc/build-msw.md) - Windows, native MSYS2 or cross-compile from Linux
* [doc/build-unix.md](doc/build-unix.md) - Linux and other Unix-like systems
* [doc/build-osx.md](doc/build-osx.md) - macOS

Berkeley DB 4.8 is required for wallet compatibility. Newer Berkeley DB
versions change the wallet file format and must not be used.

Repository layout
-----------------

    bitcoin-qt.pro     qmake project for the Qt wallet
    src/               daemon sources, RPC, wallet, script engine
    src/leveldb/       bundled LevelDB
    src/qt/            Qt wallet sources, forms, resources, translations
    doc/               build instructions and developer documentation
    share/             packaging and build helper scripts

License
-------

Bells is released under the MIT license. See [COPYING](COPYING) for details.

    Copyright (c) 2009-2014 Bitcoin Developers
    Copyright (c) 2011-2014 Bells Developers

This product includes software developed by the OpenSSL Project for use in the
OpenSSL Toolkit (http://www.openssl.org/), cryptographic software written by
Eric Young (eay@cryptsoft.com), and UPnP software written by Thomas Bernard.
