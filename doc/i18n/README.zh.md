# Bells (BEL)

Bells 是一个去中心化的点对点电子现金系统，工作量证明采用 **scrypt** 算法。
本项目分叉自 Litecoin：出块时间 2.5 分钟，每个区块重新调整难度（DigiShield），
总供应量 500,000,000 BEL。0.8.7.1 参考客户端包含守护进程 `bellsd` 和图形钱包
`bells-qt`。

## 网络参数

| 参数 | 值 |
| --- | --- |
| 工作量证明 | scrypt |
| 目标出块时间 | 2.5 分钟 |
| 难度调整 | 每个区块（DigiShield） |
| 总供应量 | 500,000,000 BEL |
| P2P 端口（主网） | 19919 |
| RPC 端口（主网） | 19918 |
| 测试网（P2P / RPC） | 29919 / 29918 |
| 地址前缀 | `B` |
| 协议版本 | 70002 |
| 数据目录（Windows） | `%APPDATA%\Bells` |
| 数据目录（Unix） | `~/.bells` |
| 配置文件 | `bells.conf` |

## Windows 快速开始

1. 从发布页面下载 `bells-0.8.7.1-win64.zip` 或 `bells-0.8.7.1-win32.zip`。
2. 将压缩包解压到一个文件夹，并保持所有文件在一起：缺少 Qt DLL 和
   `platforms` 目录时钱包无法启动。
3. 运行 `bells-qt.exe` 启动图形钱包，或运行 `bellsd.exe` 启动命令行守护进程。
4. 在使用真实资金前备份 `wallet.dat`，文件位于 `%APPDATA%\Bells`。

按 `Ctrl+C` 可停止守护进程。Windows 不支持 Unix 风格的守护进程模式，
`-daemon` 参数无效，请改用 `start /b bellsd.exe`。

## 配置

`%APPDATA%\Bells\bells.conf` 支持以下设置：

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

## 从源码构建

已验证的版本：GCC 13.2（MinGW-w64）、Boost 1.83、Berkeley DB 4.8.30、
OpenSSL 1.0.2u、Qt 5.15.2 以及随源码附带的 LevelDB。详细文档为英文：

* [Windows](../build-msw.md) - 从 Linux 交叉编译（x86_64 和 i686）
* [Unix](../build-unix.md)
* [macOS](../build-osx.md)
* [Qt 钱包](../readme-qt.rst)

必须使用 Berkeley DB 4.8：更高版本会改变 `wallet.dat` 的文件格式。

## 链接

* 网站：<http://www.bellscoin.org>
* 发布：<https://github.com/bells-coin/bells-coin/releases>

## 许可证

MIT，详见 [COPYING](../../COPYING)。
