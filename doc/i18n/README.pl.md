# Bells (BEL)

Bells to zdecentralizowany system elektronicznej gotówki działający w sieci
peer-to-peer, w którym dowód pracy opiera się na algorytmie **scrypt**. Projekt
jest forkiem Litecoina: bloki co 2,5 minuty, przeliczanie trudności w każdym
bloku (DigiShield) i całkowita podaż 500 000 000 BEL. Klient referencyjny 0.8.7.1
zawiera demona `bellsd` oraz graficzny portfel `bells-qt`.

## Parametry sieci

| Parametr | Wartość |
| --- | --- |
| Dowód pracy | scrypt |
| Docelowy czas bloku | 2,5 minuty |
| Przeliczanie trudności | w każdym bloku (DigiShield) |
| Całkowita podaż | 500 000 000 BEL |
| Port P2P (sieć główna) | 19919 |
| Port RPC (sieć główna) | 19918 |
| Sieć testowa (P2P / RPC) | 29919 / 29918 |
| Prefiks adresu | `B` |
| Wersja protokołu | 70002 |
| Katalog danych (Windows) | `%APPDATA%\Bells` |
| Katalog danych (Unix) | `~/.bells` |
| Plik konfiguracyjny | `bells.conf` |

## Szybki start w systemie Windows

1. Pobierz `bells-0.8.7.1-win64.zip` lub `bells-0.8.7.1-win32.zip` ze strony
   wydań.
2. Rozpakuj archiwum do folderu i trzymaj wszystkie pliki razem: bez bibliotek
   Qt i folderu `platforms` portfel się nie uruchomi.
3. Uruchom `bells-qt.exe` dla portfela graficznego albo `bellsd.exe` dla demona
   w wierszu poleceń.
4. Zrób kopię zapasową `wallet.dat`, zanim użyjesz portfela z prawdziwymi
   środkami. Plik znajduje się w `%APPDATA%\Bells`.

Demon zatrzymuje się po naciśnięciu `Ctrl+C`. Windows nie obsługuje demonizacji
w stylu Unix, więc opcja `-daemon` nie działa; użyj `start /b bellsd.exe`.

## Konfiguracja

Plik `%APPDATA%\Bells\bells.conf` przyjmuje następujące ustawienia:

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

## Kompilacja ze źródeł

Przetestowane wersje: GCC 13.2 (MinGW-w64), Boost 1.83, Berkeley DB 4.8.30,
OpenSSL 1.0.2u, Qt 5.15.2 oraz dołączony LevelDB. Szczegółowa dokumentacja jest
w języku angielskim:

* [Windows](../build-msw.md) - kompilacja krzyżowa z Linuksa (x86_64 i i686)
* [Unix](../build-unix.md)
* [macOS](../build-osx.md)
* [Portfel Qt](../readme-qt.rst)

Berkeley DB 4.8 jest wymagana: nowsze wersje zmieniają format pliku
`wallet.dat`.

## Odnośniki

* Strona: <http://www.bellscoin.org>
* Wydania: <https://github.com/bells-coin/bells-coin/releases>

## Licencja

MIT. Zobacz [COPYING](../../COPYING).
