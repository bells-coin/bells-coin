# Bells (BEL)

Bells on hajautettu vertaisverkkoon perustuva sähköinen käteisjärjestelmä,
jonka työtodistus perustuu **scrypt**-algoritmiin. Projekti on Litecoinin
haarautuma: 2,5 minuutin lohkot, vaikeustason säätö jokaisessa lohkossa
(DigiShield) ja kokonaismäärä 500 000 000 BEL. Vertailuasiakas 0.8.7.1 sisältää
`bellsd`-taustapalvelun ja `bells-qt`-graafisen lompakon.

## Verkon parametrit

| Parametri | Arvo |
| --- | --- |
| Työtodistus | scrypt |
| Tavoitelohkoaika | 2,5 minuuttia |
| Vaikeustason säätö | jokaisessa lohkossa (DigiShield) |
| Kokonaismäärä | 500 000 000 BEL |
| P2P-portti (pääverkko) | 19919 |
| RPC-portti (pääverkko) | 19918 |
| Testiverkko (P2P / RPC) | 29919 / 29918 |
| Osoitteen etuliite | `B` |
| Protokollan versio | 70002 |
| Datakansio (Windows) | `%APPDATA%\Bells` |
| Datakansio (Unix) | `~/.bells` |
| Asetustiedosto | `bells.conf` |

## Pika-aloitus Windowsissa

1. Lataa `bells-0.8.7.1-win64.zip` tai `bells-0.8.7.1-win32.zip` julkaisusivulta.
2. Pura arkisto kansioon ja pidä kaikki tiedostot yhdessä: ilman Qt-DLL:iä ja
   `platforms`-kansiota lompakko ei käynnisty.
3. Käynnistä `bells-qt.exe` graafista lompakkoa varten tai `bellsd.exe`
   komentorivin taustapalvelua varten.
4. Varmuuskopioi `wallet.dat` ennen kuin käytät lompakkoa oikeilla varoilla.
   Tiedosto sijaitsee kansiossa `%APPDATA%\Bells`.

Taustapalvelu pysäytetään painamalla `Ctrl+C`. Windowsissa ei ole Unix-tyylistä
taustapalvelutilaa, joten `-daemon`-valitsimella ei ole vaikutusta; käytä
komentoa `start /b bellsd.exe`.

## Asetukset

Tiedosto `%APPDATA%\Bells\bells.conf` hyväksyy muun muassa:

```ini
server=1
rpcuser=kayttaja
rpcpassword=vaihda-tama
rpcallowip=127.0.0.1
rpcport=19918
port=19919
# addnode=1.2.3.4:19919
# listen=1
```

## Kääntäminen lähdekoodista

Testatut versiot: GCC 13.2 (MinGW-w64), Boost 1.83, Berkeley DB 4.8.30,
OpenSSL 1.0.2u, Qt 5.15.2 ja mukana tuleva LevelDB. Täydellinen dokumentaatio on
englanniksi:

* [Windows](../build-msw.md) — ristikääntäminen Linuxista (x86_64 ja i686)
* [Unix](../build-unix.md)
* [macOS](../build-osx.md)
* [Qt-lompakko](../readme-qt.rst)

Berkeley DB 4.8 on pakollinen: uudemmat versiot muuttavat `wallet.dat`-tiedoston
muotoa.

## Linkit

* Verkkosivusto: <http://www.bellscoin.org>
* Julkaisut: <https://github.com/bells-coin/bells-coin/releases>

## Lisenssi

MIT. Katso [COPYING](../../COPYING).
