# Bells (BEL)

Bells est une monnaie électronique pair-à-pair décentralisée dont la preuve de
travail repose sur l'algorithme **scrypt**. Le projet est un fork de Litecoin :
blocs de 2,5 minutes, réajustement de la difficulté à chaque bloc (DigiShield)
et une offre totale de 500 000 000 BEL. Le client de référence 0.8.7.1 fournit
le démon `bellsd` et le portefeuille graphique `bells-qt`.

## Paramètres du réseau

| Paramètre | Valeur |
| --- | --- |
| Preuve de travail | scrypt |
| Temps de bloc cible | 2,5 minutes |
| Réajustement de la difficulté | à chaque bloc (DigiShield) |
| Offre totale | 500 000 000 BEL |
| Port P2P (réseau principal) | 19919 |
| Port RPC (réseau principal) | 19918 |
| Réseau de test (P2P / RPC) | 29919 / 29918 |
| Préfixe d'adresse | `B` |
| Version du protocole | 70002 |
| Répertoire de données (Windows) | `%APPDATA%\Bells` |
| Répertoire de données (Unix) | `~/.bells` |
| Fichier de configuration | `bells.conf` |

## Démarrage rapide sous Windows

1. Téléchargez `bells-0.8.7.1-win64.zip` ou `bells-0.8.7.1-win32.zip` depuis la
   page des versions.
2. Décompressez l'archive dans un dossier et conservez tous les fichiers
   ensemble : sans les DLL Qt ni le dossier `platforms`, le portefeuille ne
   démarre pas.
3. Lancez `bells-qt.exe` pour le portefeuille graphique ou `bellsd.exe` pour le
   démon en ligne de commande.
4. Sauvegardez `wallet.dat` avant d'utiliser le portefeuille avec de vrais
   fonds. Le fichier se trouve dans `%APPDATA%\Bells`.

Le démon s'arrête avec `Ctrl+C`. La démonisation de type Unix n'existe pas sous
Windows : l'option `-daemon` est sans effet, utilisez `start /b bellsd.exe`.

## Configuration

Le fichier `%APPDATA%\Bells\bells.conf` accepte les paramètres suivants :

```ini
server=1
rpcuser=utilisateur
rpcpassword=changez-moi
rpcallowip=127.0.0.1
rpcport=19918
port=19919
# addnode=1.2.3.4:19919
# listen=1
```

## Compilation depuis les sources

Versions testées : GCC 13.2 (MinGW-w64), Boost 1.83, Berkeley DB 4.8.30,
OpenSSL 1.0.2u, Qt 5.15.2 et LevelDB intégré. La documentation complète est en
anglais :

* [Windows](../build-msw.md) — compilation croisée depuis Linux (x86_64 et i686)
* [Unix](../build-unix.md)
* [macOS](../build-osx.md)
* [Portefeuille Qt](../readme-qt.rst)

Berkeley DB 4.8 est obligatoire : les versions plus récentes modifient le format
du fichier `wallet.dat`.

## Liens

* Site web : <http://www.bellscoin.org>
* Versions : <https://github.com/bells-coin/bells-coin/releases>

## Licence

MIT. Voir [COPYING](../../COPYING).
