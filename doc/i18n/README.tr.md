# Bells (BEL)

Bells, iş kanıtı olarak **scrypt** algoritmasını kullanan, eşten eşe çalışan
merkeziyetsiz bir elektronik nakit sistemidir. Proje Litecoin'den çatallanmıştır:
2,5 dakikalık bloklar, her blokta zorluk yeniden ayarı (DigiShield) ve toplam
500.000.000 BEL arz. 0.8.7.1 referans istemcisi `bellsd` sunucusunu ve
`bells-qt` grafik cüzdanını içerir.

## Ağ parametreleri

| Parametre | Değer |
| --- | --- |
| İş kanıtı | scrypt |
| Hedef blok süresi | 2,5 dakika |
| Zorluk yeniden ayarı | her blokta (DigiShield) |
| Toplam arz | 500.000.000 BEL |
| P2P bağlantı noktası (ana ağ) | 19919 |
| RPC bağlantı noktası (ana ağ) | 19918 |
| Test ağı (P2P / RPC) | 29919 / 29918 |
| Adres öneki | `B` |
| Protokol sürümü | 70002 |
| Veri dizini (Windows) | `%APPDATA%\Bells` |
| Veri dizini (Unix) | `~/.bells` |
| Yapılandırma dosyası | `bells.conf` |

## Windows'ta hızlı başlangıç

1. Sürümler sayfasından `bells-0.8.7.1-win64.zip` veya
   `bells-0.8.7.1-win32.zip` dosyasını indirin.
2. Arşivi bir klasöre açın ve tüm dosyaları bir arada tutun: Qt DLL'leri ve
   `platforms` klasörü olmadan cüzdan açılmaz.
3. Grafik cüzdan için `bells-qt.exe`, komut satırı sunucusu için `bellsd.exe`
   çalıştırın.
4. Cüzdanı gerçek bakiyeyle kullanmadan önce `wallet.dat` dosyasını yedekleyin.
   Dosya `%APPDATA%\Bells` içindedir.

Sunucu `Ctrl+C` ile durdurulur. Windows, Unix tarzı arka plan sunucu modunu
desteklemez; `-daemon` seçeneğinin etkisi yoktur, bunun yerine
`start /b bellsd.exe` kullanın.

## Yapılandırma

`%APPDATA%\Bells\bells.conf` dosyası şu ayarları kabul eder:

```ini
server=1
rpcuser=kullanici
rpcpassword=degistir
rpcallowip=127.0.0.1
rpcport=19918
port=19919
# addnode=1.2.3.4:19919
# listen=1
```

## Kaynaktan derleme

Denenen sürümler: GCC 13.2 (MinGW-w64), Boost 1.83, Berkeley DB 4.8.30,
OpenSSL 1.0.2u, Qt 5.15.2 ve paket içindeki LevelDB. Ayrıntılı belgeler
İngilizcedir:

* [Windows](../build-msw.md) - Linux'tan çapraz derleme (x86_64 ve i686)
* [Unix](../build-unix.md)
* [macOS](../build-osx.md)
* [Qt cüzdanı](../readme-qt.rst)

Berkeley DB 4.8 zorunludur: daha yeni sürümler `wallet.dat` dosya biçimini
değiştirir.

## Bağlantılar

* Web sitesi: <http://www.bellscoin.org>
* Sürümler: <https://github.com/bells-coin/bells-coin/releases>

## Lisans

MIT. Bkz. [COPYING](../../COPYING).
