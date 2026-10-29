# Bells (BEL)

Bells는 **scrypt** 알고리즘을 작업 증명으로 사용하는 탈중앙화 P2P 전자 화폐
시스템입니다. Litecoin에서 포크된 프로젝트로, 블록 생성 간격은 2.5분, 난이도는
매 블록마다 재조정되며(DigiShield), 총 발행량은 500,000,000 BEL입니다. 0.8.7.1
참조 클라이언트는 `bellsd` 데몬과 `bells-qt` 그래픽 지갑으로 구성됩니다.

## 네트워크 매개변수

| 매개변수 | 값 |
| --- | --- |
| 작업 증명 | scrypt |
| 목표 블록 시간 | 2.5분 |
| 난이도 재조정 | 매 블록 (DigiShield) |
| 총 발행량 | 500,000,000 BEL |
| P2P 포트 (메인넷) | 19919 |
| RPC 포트 (메인넷) | 19918 |
| 테스트넷 (P2P / RPC) | 29919 / 29918 |
| 주소 접두사 | `B` |
| 프로토콜 버전 | 70002 |
| 데이터 디렉터리 (Windows) | `%APPDATA%\Bells` |
| 데이터 디렉터리 (Unix) | `~/.bells` |
| 설정 파일 | `bells.conf` |

## Windows 빠른 시작

1. 릴리스 페이지에서 `bells-0.8.7.1-win64.zip` 또는
   `bells-0.8.7.1-win32.zip`을 내려받습니다.
2. 압축을 폴더에 풀고 모든 파일을 함께 보관합니다. Qt DLL과 `platforms`
   폴더가 없으면 지갑이 실행되지 않습니다.
3. 그래픽 지갑은 `bells-qt.exe`, 명령줄 데몬은 `bellsd.exe`를 실행합니다.
4. 실제 자금으로 지갑을 사용하기 전에 `wallet.dat`을 백업하십시오. 파일은
   `%APPDATA%\Bells`에 있습니다.

데몬은 `Ctrl+C`로 중지합니다. Windows에는 Unix 방식의 데몬화가 없으므로
`-daemon` 옵션은 효과가 없습니다. 대신 `start /b bellsd.exe`를 사용하십시오.

## 설정

`%APPDATA%\Bells\bells.conf`에서 다음을 설정할 수 있습니다:

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

## 소스에서 빌드

검증된 버전: GCC 13.2(MinGW-w64), Boost 1.83, Berkeley DB 4.8.30,
OpenSSL 1.0.2u, Qt 5.15.2, 포함된 LevelDB. 자세한 문서는 영어로 제공됩니다:

* [Windows](../build-msw.md) - Linux에서 크로스 컴파일(x86_64 및 i686)
* [Unix](../build-unix.md)
* [macOS](../build-osx.md)
* [Qt 지갑](../readme-qt.rst)

Berkeley DB 4.8이 필수입니다. 최신 버전은 `wallet.dat` 파일 형식을 변경합니다.

## 링크

* 웹사이트: <http://www.bellscoin.org>
* 릴리스: <https://github.com/bells-coin/bells-coin/releases>

## 라이선스

MIT. [COPYING](../../COPYING)을 참조하십시오.
