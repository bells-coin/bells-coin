Bells 0.8.7.1
=============

Copyright (c) 2009-2014 Bitcoin Developers
Copyright (c) 2011-2014 Bells Developers

Distributed under the MIT/X11 software license, see the accompanying
file COPYING or http://www.opensource.org/licenses/mit-license.php.
This product includes software developed by the OpenSSL Project for use in the [OpenSSL Toolkit](http://www.openssl.org/). This product includes
cryptographic software written by Eric Young ([eay@cryptsoft.com](mailto:eay@cryptsoft.com)), and UPnP software written by Thomas Bernard.


Intro
---------------------
Bells is a free open source peer-to-peer electronic cash system that is
completely decentralized, without the need for a central server or trusted
parties. Users hold the crypto keys to their own money and transact directly
with each other, with the help of a P2P network to check for double-spending.

This is the 0.8.x reference implementation: `bellsd` (daemon) and `bells-qt`
(graphical wallet). See the top level [README](../README.md) for the coin
parameters, the project status and the end user instructions.


Setup
---------------------
Windows users can download a ready to use archive from the releases page and
unpack it into any directory:

- `bells-qt.exe` - graphical wallet
- `bellsd.exe` - headless daemon

Both executables need the bundled Qt libraries and the `platforms` directory
next to them. The data directory is `%APPDATA%\Bells` on Windows and
`~/.bells` on Unix-like systems.

On Linux the wallet needs the Qt 5 runtime libraries installed by the
distribution, for example `libqt5widgets5`, `libqt5gui5` and `libqt5network5`.


Other Pages
---------------------
- [Translations](i18n/README.md)
- [Windows Build Notes](build-msw.md)
- [Unix Build Notes](build-unix.md)
- [OSX Build Notes](build-osx.md)
- [Qt Wallet Notes](readme-qt.rst)
- [Coding Guidelines](coding.md)
- [Release Process](release-process.md)
- [Release Notes](release-notes.md)
- [Multiwallet Qt Development](multiwallet-qt.md)
- [Unit Tests](unit-tests.md)
- [Translation Process](translation_process.md)
- [Tor Support](Tor.txt)
