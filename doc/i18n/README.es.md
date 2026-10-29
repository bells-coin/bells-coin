# Bells (BEL)

Bells es un sistema de efectivo electrónico descentralizado entre pares
(peer-to-peer) cuya prueba de trabajo utiliza el algoritmo **scrypt**. El
proyecto es un fork de Litecoin: bloques de 2,5 minutos, reajuste de dificultad
en cada bloque (DigiShield) y un suministro total de 500.000.000 BEL. El cliente
de referencia 0.8.7.1 incluye el demonio `bellsd` y el monedero gráfico
`bells-qt`.

## Parámetros de la red

| Parámetro | Valor |
| --- | --- |
| Prueba de trabajo | scrypt |
| Tiempo de bloque objetivo | 2,5 minutos |
| Reajuste de dificultad | cada bloque (DigiShield) |
| Suministro total | 500.000.000 BEL |
| Puerto P2P (red principal) | 19919 |
| Puerto RPC (red principal) | 19918 |
| Red de pruebas (P2P / RPC) | 29919 / 29918 |
| Prefijo de dirección | `B` |
| Versión del protocolo | 70002 |
| Directorio de datos (Windows) | `%APPDATA%\Bells` |
| Directorio de datos (Unix) | `~/.bells` |
| Archivo de configuración | `bells.conf` |

## Inicio rápido en Windows

1. Descargue `bells-0.8.7.1-win64.zip` o `bells-0.8.7.1-win32.zip` desde la
   página de versiones.
2. Extraiga el archivo en una carpeta y mantenga todos los archivos juntos: sin
   las DLL de Qt ni la carpeta `platforms` el monedero no arranca.
3. Ejecute `bells-qt.exe` para el monedero gráfico o `bellsd.exe` para el
   demonio en la línea de comandos.
4. Haga una copia de `wallet.dat` antes de usar el monedero con fondos reales.
   El archivo está en `%APPDATA%\Bells`.

El demonio se detiene con `Ctrl+C`. Windows no admite el modo demonio de Unix:
la opción `-daemon` no tiene efecto, use `start /b bellsd.exe`.

## Configuración

El archivo `%APPDATA%\Bells\bells.conf` acepta, entre otros:

```ini
server=1
rpcuser=usuario
rpcpassword=cambiar
rpcallowip=127.0.0.1
rpcport=19918
port=19919
# addnode=1.2.3.4:19919
# listen=1
```

## Compilar desde el código fuente

Versiones probadas: GCC 13.2 (MinGW-w64), Boost 1.83, Berkeley DB 4.8.30,
OpenSSL 1.0.2u, Qt 5.15.2 y el LevelDB incluido. La documentación completa está
en inglés:

* [Windows](../build-msw.md) — compilación cruzada desde Linux (x86_64 e i686)
* [Unix](../build-unix.md)
* [macOS](../build-osx.md)
* [Monedero Qt](../readme-qt.rst)

Berkeley DB 4.8 es obligatorio: las versiones más recientes cambian el formato
de `wallet.dat`.

## Enlaces

* Sitio web: <http://www.bellscoin.org>
* Versiones: <https://github.com/bells-coin/bells-coin/releases>

## Licencia

MIT. Consulte [COPYING](../../COPYING).
