# Bells (BEL)

A Bells egy decentralizált, peer-to-peer elektronikus készpénzrendszer, amelynek
munkabizonyítéka a **scrypt** algoritmuson alapul. A projekt a Litecoin forkja:
2,5 perces blokkok, minden blokkban újraszámolt nehézség (DigiShield) és
500 000 000 BEL teljes kibocsátás. A 0.8.7.1 referenciaügyfél a `bellsd` démont
és a `bells-qt` grafikus tárcát tartalmazza.

## Hálózati paraméterek

| Paraméter | Érték |
| --- | --- |
| Munkabizonyíték | scrypt |
| Cél blokkidő | 2,5 perc |
| Nehézség újraszámítása | minden blokkban (DigiShield) |
| Teljes kibocsátás | 500 000 000 BEL |
| P2P port (főhálózat) | 19919 |
| RPC port (főhálózat) | 19918 |
| Teszthálózat (P2P / RPC) | 29919 / 29918 |
| Cím előtag | `B` |
| Protokoll verzió | 70002 |
| Adatkönyvtár (Windows) | `%APPDATA%\Bells` |
| Adatkönyvtár (Unix) | `~/.bells` |
| Konfigurációs fájl | `bells.conf` |

## Gyors indítás Windows alatt

1. Töltse le a `bells-0.8.7.1-win64.zip` vagy `bells-0.8.7.1-win32.zip`
   csomagot a kiadások oldaláról.
2. Csomagolja ki egy mappába, és tartsa együtt az összes fájlt: a Qt DLL-ek és a
   `platforms` mappa nélkül a tárca nem indul el.
3. Indítsa el a `bells-qt.exe` fájlt a grafikus tárcához, vagy a `bellsd.exe`
   fájlt a parancssori démonhoz.
4. Készítsen biztonsági másolatot a `wallet.dat` fájlról, mielőtt valódi
   egyenleggel használja a tárcát. A fájl a `%APPDATA%\Bells` mappában található.

A démon `Ctrl+C` billentyűkombinációval állítható le. A Windows nem támogatja a
Unix típusú démonizálást, ezért a `-daemon` kapcsolónak nincs hatása; használja a
`start /b bellsd.exe` parancsot.

## Konfiguráció

A `%APPDATA%\Bells\bells.conf` fájl a következő beállításokat fogadja el:

```ini
server=1
rpcuser=user
rpcpassword=change-me
rpcallowip=127.0.0.1
rpcport=19918
port=19919
# addnode=1.2.3.4:19919
# listen=1
```

## Fordítás forráskódból

Tesztelt verziók: GCC 13.2 (MinGW-w64), Boost 1.83, Berkeley DB 4.8.30,
OpenSSL 1.0.2u, Qt 5.15.2 és a mellékelt LevelDB. A részletes dokumentáció
angol nyelven érhető el:

* [Windows](../build-msw.md) - kereszfordítás Linuxról (x86_64 és i686)
* [Unix](../build-unix.md)
* [macOS](../build-osx.md)
* [Qt tárca](../readme-qt.rst)

A Berkeley DB 4.8 kötelező: az újabb verziók megváltoztatják a `wallet.dat`
fájlformátumát.

## Hivatkozások

* Webhely: <http://www.bellscoin.org>
* Kiadások: <https://github.com/bells-coin/bells-coin/releases>

## Licenc

MIT. Lásd: [COPYING](../../COPYING).
