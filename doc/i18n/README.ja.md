# Bells (BEL)

Bells は、**scrypt** をプルーフ・オブ・ワークに採用した分散型のピアツーピア
電子決済システムです。Litecoin からのフォークで、ブロック生成間隔は 2.5 分、
難易度は毎ブロック再計算され（DigiShield）、総供給量は 500,000,000 BEL です。
リファレンスクライアント 0.8.7.1 はデーモン `bellsd` と GUI ウォレット
`bells-qt` で構成されます。

## ネットワークパラメータ

| パラメータ | 値 |
| --- | --- |
| プルーフ・オブ・ワーク | scrypt |
| 目標ブロック時間 | 2.5 分 |
| 難易度調整 | 毎ブロック（DigiShield） |
| 総供給量 | 500,000,000 BEL |
| P2P ポート（メインネット） | 19919 |
| RPC ポート（メインネット） | 19918 |
| テストネット（P2P / RPC） | 29919 / 29918 |
| アドレス接頭辞 | `B` |
| プロトコルバージョン | 70002 |
| データディレクトリ（Windows） | `%APPDATA%\Bells` |
| データディレクトリ（Unix） | `~/.bells` |
| 設定ファイル | `bells.conf` |

## Windows でのクイックスタート

1. リリースページから `bells-0.8.7.1-win64.zip` または
   `bells-0.8.7.1-win32.zip` をダウンロードします。
2. アーカイブをフォルダに展開し、すべてのファイルを同じ場所に置きます。
   Qt の DLL と `platforms` フォルダがないとウォレットは起動しません。
3. GUI ウォレットは `bells-qt.exe`、コマンドラインのデーモンは `bellsd.exe`
   を実行します。
4. 実際の資金でウォレットを使う前に `wallet.dat` をバックアップしてください。
   ファイルは `%APPDATA%\Bells` にあります。

デーモンは `Ctrl+C` で停止します。Windows には Unix 形式のデーモン化がない
ため `-daemon` は効果がありません。`start /b bellsd.exe` を使用してください。

## 設定

`%APPDATA%\Bells\bells.conf` では次の設定を使用できます:

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

## ソースからのビルド

動作確認済みのバージョン: GCC 13.2（MinGW-w64）、Boost 1.83、
Berkeley DB 4.8.30、OpenSSL 1.0.2u、Qt 5.15.2、同梱の LevelDB。
詳細なドキュメントは英語です:

* [Windows](../build-msw.md) - Linux からのクロスコンパイル（x86_64 / i686）
* [Unix](../build-unix.md)
* [macOS](../build-osx.md)
* [Qt ウォレット](../readme-qt.rst)

Berkeley DB 4.8 は必須です。新しいバージョンは `wallet.dat` の形式を変更します。

## リンク

* ウェブサイト: <http://www.bellscoin.org>
* リリース: <https://github.com/bells-coin/bells-coin/releases>

## ライセンス

MIT。[COPYING](../../COPYING) を参照してください。
