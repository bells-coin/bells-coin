# Bells (BEL)

Bells è un sistema di moneta elettronica decentralizzato peer-to-peer con
**scrypt** come prova di lavoro. Il progetto è un fork di Litecoin: blocchi da
2,5 minuti, ricalcolo della difficoltà a ogni blocco (DigiShield) e una
emissione totale di 500.000.000 BEL. Il client di riferimento 0.8.7.1 comprende
il demone `bellsd` e il portafoglio grafico `bells-qt`.

## Parametri della rete

| Parametro | Valore |
| --- | --- |
| Prova di lavoro | scrypt |
| Tempo di blocco previsto | 2,5 minuti |
| Ricalcolo della difficoltà | a ogni blocco (DigiShield) |
| Emissione totale | 500.000.000 BEL |
| Porta P2P (rete principale) | 19919 |
| Porta RPC (rete principale) | 19918 |
| Rete di test (P2P / RPC) | 29919 / 29918 |
| Prefisso degli indirizzi | `B` |
| Versione del protocollo | 70002 |
| Cartella dati (Windows) | `%APPDATA%\Bells` |
| Cartella dati (Unix) | `~/.bells` |
| File di configurazione | `bells.conf` |

## Avvio rapido su Windows

1. Scaricare `bells-0.8.7.1-win64.zip` o `bells-0.8.7.1-win32.zip` dalla pagina
   delle release.
2. Estrarre l'archivio in una cartella e tenere tutti i file insieme: senza le
   DLL di Qt e la cartella `platforms` il portafoglio non si avvia.
3. Avviare `bells-qt.exe` per il portafoglio grafico oppure `bellsd.exe` per il
   demone da riga di comando.
4. Fare una copia di `wallet.dat` prima di usare il portafoglio con fondi reali.
   Il file si trova in `%APPDATA%\Bells`.

Il demone si arresta con `Ctrl+C`. Windows non supporta la modalità demone di
Unix: l'opzione `-daemon` non ha effetto, usare `start /b bellsd.exe`.

## Configurazione

Il file `%APPDATA%\Bells\bells.conf` accetta, tra gli altri:

```ini
server=1
rpcuser=utente
rpcpassword=cambiare
rpcallowip=127.0.0.1
rpcport=19918
port=19919
# addnode=1.2.3.4:19919
# listen=1
```

## Compilazione dai sorgenti

Versioni testate: GCC 13.2 (MinGW-w64), Boost 1.83, Berkeley DB 4.8.30,
OpenSSL 1.0.2u, Qt 5.15.2 e il LevelDB incluso. La documentazione completa è in
inglese:

* [Windows](../build-msw.md) — compilazione incrociata da Linux (x86_64 e i686)
* [Unix](../build-unix.md)
* [macOS](../build-osx.md)
* [Portafoglio Qt](../readme-qt.rst)

Berkeley DB 4.8 è obbligatorio: le versioni più recenti cambiano il formato di
`wallet.dat`.

## Collegamenti

* Sito web: <http://www.bellscoin.org>
* Release: <https://github.com/bells-coin/bells-coin/releases>

## Licenza

MIT. Vedere [COPYING](../../COPYING).
