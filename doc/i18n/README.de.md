# Bells (BEL)

Bells ist ein dezentrales Peer-to-Peer-Zahlungssystem mit **scrypt** als
Proof-of-Work. Das Projekt ist ein Fork von Litecoin: 2,5-Minuten-Blöcke,
Neuberechnung der Schwierigkeit in jedem Block (DigiShield) und eine
Gesamtmenge von 500.000.000 BEL. Der Referenzclient 0.8.7.1 besteht aus dem
Daemon `bellsd` und der grafischen Wallet `bells-qt`.

## Netzwerkparameter

| Parameter | Wert |
| --- | --- |
| Proof-of-Work | scrypt |
| Ziel-Blockzeit | 2,5 Minuten |
| Schwierigkeitsanpassung | jeder Block (DigiShield) |
| Gesamtmenge | 500.000.000 BEL |
| P2P-Port (Mainnet) | 19919 |
| RPC-Port (Mainnet) | 19918 |
| Testnet (P2P / RPC) | 29919 / 29918 |
| Adresspräfix | `B` |
| Protokollversion | 70002 |
| Datenverzeichnis (Windows) | `%APPDATA%\Bells` |
| Datenverzeichnis (Unix) | `~/.bells` |
| Konfigurationsdatei | `bells.conf` |

## Schnellstart unter Windows

1. Laden Sie `bells-0.8.7.1-win64.zip` oder `bells-0.8.7.1-win32.zip` von der
   Releases-Seite herunter.
2. Entpacken Sie das Archiv in einen Ordner und lassen Sie alle Dateien
   zusammen: ohne die Qt-DLLs und den Ordner `platforms` startet die Wallet
   nicht.
3. Starten Sie `bells-qt.exe` für die grafische Wallet oder `bellsd.exe` für den
   Daemon auf der Kommandozeile.
4. Sichern Sie `wallet.dat`, bevor Sie die Wallet mit echten Guthaben nutzen.
   Die Datei liegt in `%APPDATA%\Bells`.

Der Daemon wird mit `Ctrl+C` beendet. Unter Windows gibt es keine
Unix-Daemonisierung, die Option `-daemon` hat keine Wirkung; verwenden Sie
`start /b bellsd.exe`.

## Konfiguration

Die Datei `%APPDATA%\Bells\bells.conf` akzeptiert unter anderem:

```ini
server=1
rpcuser=benutzer
rpcpassword=aendern
rpcallowip=127.0.0.1
rpcport=19918
port=19919
# addnode=1.2.3.4:19919
# listen=1
```

## Aus dem Quellcode bauen

Getestete Versionen: GCC 13.2 (MinGW-w64), Boost 1.83, Berkeley DB 4.8.30,
OpenSSL 1.0.2u, Qt 5.15.2 und das mitgelieferte LevelDB. Die vollständige
Dokumentation ist auf Englisch verfügbar:

* [Windows](../build-msw.md) — Cross-Compilation unter Linux (x86_64 und i686)
* [Unix](../build-unix.md)
* [macOS](../build-osx.md)
* [Qt-Wallet](../readme-qt.rst)

Berkeley DB 4.8 ist zwingend erforderlich: neuere Versionen ändern das Format
von `wallet.dat`.

## Links

* Website: <http://www.bellscoin.org>
* Releases: <https://github.com/bells-coin/bells-coin/releases>

## Lizenz

MIT. Siehe [COPYING](../../COPYING).
