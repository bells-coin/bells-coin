# Bells documentation in other languages
======================================

The English [README](../../README.md) and the build instructions in
[doc/](../README.md) are the reference documentation. The pages below are
self-contained translations of the project description and the end user
instructions. They may lag behind the English original after an update.

## Available languages

| Language | Native name | Code | File |
| --- | --- | --- | --- |
| Arabic | العربية | `ar` | [README.ar.md](README.ar.md) |
| Bengali | বাংলা | `bn` | [README.bn.md](README.bn.md) |
| Bulgarian | Български | `bg` | [README.bg.md](README.bg.md) |
| Chinese (Simplified) | 简体中文 | `zh` | [README.zh.md](README.zh.md) |
| Finnish | Suomi | `fi` | [README.fi.md](README.fi.md) |
| French | Français | `fr` | [README.fr.md](README.fr.md) |
| German | Deutsch | `de` | [README.de.md](README.de.md) |
| Hindi | हिन्दी | `hi` | [README.hi.md](README.hi.md) |
| Hungarian | Magyar | `hu` | [README.hu.md](README.hu.md) |
| Indonesian | Bahasa Indonesia | `id` | [README.id.md](README.id.md) |
| Italian | Italiano | `it` | [README.it.md](README.it.md) |
| Japanese | 日本語 | `ja` | [README.ja.md](README.ja.md) |
| Korean | 한국어 | `ko` | [README.ko.md](README.ko.md) |
| Polish | Polski | `pl` | [README.pl.md](README.pl.md) |
| Portuguese | Português | `pt` | [README.pt.md](README.pt.md) |
| Russian | Русский | `ru` | [README.ru.md](README.ru.md) |
| Spanish | Español | `es` | [README.es.md](README.es.md) |
| Turkish | Türkçe | `tr` | [README.tr.md](README.tr.md) |
| Urdu | اردو | `ur` | [README.ur.md](README.ur.md) |

## Structure of each translation

Every file contains the same sections:

1. What Bells is and which client release it describes.
2. Network parameters: proof of work, block time, supply, ports, address
   prefix, protocol version, data directories and configuration file.
3. Quick start on Windows: downloading the release archive, running
   `bells-qt.exe` and `bellsd.exe`, and backing up the wallet.
4. A minimal `bells.conf` for running a node with RPC enabled.
5. Building from source and the versions the current release was built with.
6. Links and the MIT license.

## Adding a translation

Create `doc/i18n/README.<code>.md` using an ISO 639-1 language code, follow the
structure above and add a row to the table. Documentation changes are accepted
as pull requests. Please keep the terminology consistent with the English
original: `bellsd`, `bells-qt`, `bells.conf`, `wallet.dat`, `scrypt`,
`DigiShield`.
