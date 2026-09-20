# DMVPN Phase 1

GNS3上でDMVPN（Phase 1）を構築し、NHRP登録とEIGRPネイバー確立をパケットキャプチャで確認した検証の設定ファイルです。

記事：[DMVPNの仕組みをパケットで解説｜NHRP登録とEIGRP確立を検証](https://www.tech-lablog.com/dmvpn-nhrp-packet-capture/)

## 構成

![DMVPN検証構成図](https://www.tech-lablog.com/wp-content/uploads/2026/09/dmvpn-topology.png)

| 機器 | Tunnel0 | NBMA（Ethernet0/0） | LAN（Loopback1） |
|---|---|---|---|
| HUB-RT-01 | 10.0.0.1/24 | 198.51.100.1/30 | 192.168.0.1/24 |
| SPOKE-RT-01 | 10.0.0.11/24 | 198.51.100.6/30 | 192.168.1.1/24 |
| SPOKE-RT-02 | 10.0.0.12/24 | 198.51.100.10/30 | 192.168.2.1/24 |
| ISP | — | 198.51.100.2 / .5 / .9 | — |

## ファイル

| ファイル | 内容 |
|---|---|
| [configs/HUB-RT-01.cfg](./configs/HUB-RT-01.cfg) | ハブ |
| [configs/SPOKE-RT-01.cfg](./configs/SPOKE-RT-01.cfg) | スポーク1（キャプチャ取得側） |
| [configs/SPOKE-RT-02.cfg](./configs/SPOKE-RT-02.cfg) | スポーク2 |
| [configs/ISP.cfg](./configs/ISP.cfg) | インターネット役 |

※ 各設定ファイルは show running-config の出力から、未使用のインターフェースなど検証に関係しない行を省略しています。

## 検証内容

- DMVPN Phase 1（スポーク間通信もハブ経由）
- ルーティング：EIGRP（AS 100）
- tunnel key：100
- IPsec：なし
