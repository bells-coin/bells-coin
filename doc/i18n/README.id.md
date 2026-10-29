# Bells (BEL)

Bells adalah sistem uang elektronik peer-to-peer terdesentralisasi yang
menggunakan algoritme **scrypt** sebagai proof-of-work. Proyek ini adalah fork
dari Litecoin: blok 2,5 menit, penyesuaian kesulitan setiap blok (DigiShield),
dan total pasokan 500.000.000 BEL. Klien referensi 0.8.7.1 terdiri dari daemon
`bellsd` dan dompet grafis `bells-qt`.

## Parameter jaringan

| Parameter | Nilai |
| --- | --- |
| Proof-of-work | scrypt |
| Waktu blok target | 2,5 menit |
| Penyesuaian kesulitan | setiap blok (DigiShield) |
| Total pasokan | 500.000.000 BEL |
| Port P2P (jaringan utama) | 19919 |
| Port RPC (jaringan utama) | 19918 |
| Jaringan uji (P2P / RPC) | 29919 / 29918 |
| Prefiks alamat | `B` |
| Versi protokol | 70002 |
| Direktori data (Windows) | `%APPDATA%\Bells` |
| Direktori data (Unix) | `~/.bells` |
| Berkas konfigurasi | `bells.conf` |

## Mulai cepat di Windows

1. Unduh `bells-0.8.7.1-win64.zip` atau `bells-0.8.7.1-win32.zip` dari halaman
   rilis.
2. Ekstrak arsip ke sebuah folder dan simpan semua berkas bersama: tanpa DLL Qt
   dan folder `platforms`, dompet tidak akan berjalan.
3. Jalankan `bells-qt.exe` untuk dompet grafis atau `bellsd.exe` untuk daemon
   baris perintah.
4. Cadangkan `wallet.dat` sebelum menggunakan dompet dengan dana nyata. Berkas
   tersebut berada di `%APPDATA%\Bells`.

Daemon dihentikan dengan `Ctrl+C`. Windows tidak mendukung mode daemon seperti
Unix, jadi opsi `-daemon` tidak berpengaruh; gunakan `start /b bellsd.exe`.

## Konfigurasi

Berkas `%APPDATA%\Bells\bells.conf` menerima pengaturan berikut:

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

## Membangun dari kode sumber

Versi yang diuji: GCC 13.2 (MinGW-w64), Boost 1.83, Berkeley DB 4.8.30,
OpenSSL 1.0.2u, Qt 5.15.2, dan LevelDB yang disertakan. Dokumentasi lengkap
tersedia dalam bahasa Inggris:

* [Windows](../build-msw.md) - kompilasi silang dari Linux (x86_64 dan i686)
* [Unix](../build-unix.md)
* [macOS](../build-osx.md)
* [Dompet Qt](../readme-qt.rst)

Berkeley DB 4.8 wajib digunakan: versi yang lebih baru mengubah format berkas
`wallet.dat`.

## Tautan

* Situs web: <http://www.bellscoin.org>
* Rilis: <https://github.com/bells-coin/bells-coin/releases>

## Lisensi

MIT. Lihat [COPYING](../../COPYING).
