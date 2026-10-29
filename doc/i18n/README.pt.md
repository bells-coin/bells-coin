# Bells (BEL)

Bells é um sistema descentralizado de dinheiro eletrônico ponto a ponto cuja
prova de trabalho usa o algoritmo **scrypt**. O projeto é um fork do Litecoin:
blocos de 2,5 minutos, reajuste de dificuldade a cada bloco (DigiShield) e
oferta total de 500.000.000 BEL. O cliente de referência 0.8.7.1 inclui o daemon
`bellsd` e a carteira gráfica `bells-qt`.

## Parâmetros da rede

| Parâmetro | Valor |
| --- | --- |
| Prova de trabalho | scrypt |
| Tempo alvo do bloco | 2,5 minutos |
| Reajuste de dificuldade | a cada bloco (DigiShield) |
| Oferta total | 500.000.000 BEL |
| Porta P2P (rede principal) | 19919 |
| Porta RPC (rede principal) | 19918 |
| Rede de testes (P2P / RPC) | 29919 / 29918 |
| Prefixo do endereço | `B` |
| Versão do protocolo | 70002 |
| Diretório de dados (Windows) | `%APPDATA%\Bells` |
| Diretório de dados (Unix) | `~/.bells` |
| Arquivo de configuração | `bells.conf` |

## Início rápido no Windows

1. Baixe `bells-0.8.7.1-win64.zip` ou `bells-0.8.7.1-win32.zip` na página de
   versões.
2. Extraia o arquivo em uma pasta e mantenha todos os arquivos juntos: sem as
   DLLs do Qt e a pasta `platforms` a carteira não inicia.
3. Execute `bells-qt.exe` para a carteira gráfica ou `bellsd.exe` para o daemon
   na linha de comando.
4. Faça uma cópia de `wallet.dat` antes de usar a carteira com fundos reais. O
   arquivo fica em `%APPDATA%\Bells`.

O daemon é encerrado com `Ctrl+C`. O Windows não oferece o modo daemon do Unix,
portanto a opção `-daemon` não tem efeito; use `start /b bellsd.exe`.

## Configuração

O arquivo `%APPDATA%\Bells\bells.conf` aceita as seguintes opções:

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

## Compilação a partir do código-fonte

Versões testadas: GCC 13.2 (MinGW-w64), Boost 1.83, Berkeley DB 4.8.30,
OpenSSL 1.0.2u, Qt 5.15.2 e o LevelDB incluído. A documentação detalhada está em
inglês:

* [Windows](../build-msw.md) - compilação cruzada a partir do Linux (x86_64 e i686)
* [Unix](../build-unix.md)
* [macOS](../build-osx.md)
* [Carteira Qt](../readme-qt.rst)

O Berkeley DB 4.8 é obrigatório: versões mais recentes alteram o formato do
arquivo `wallet.dat`.

## Links

* Site: <http://www.bellscoin.org>
* Versões: <https://github.com/bells-coin/bells-coin/releases>

## Licença

MIT. Consulte [COPYING](../../COPYING).
