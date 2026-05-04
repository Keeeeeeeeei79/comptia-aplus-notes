# 6. トラブルシューティングコマンド — CompTIA A+ 220-1201 — 2.8 / 5.5

**Source:** Professor Messer  
**URL:**
- [Network Tools — 2.8](https://www.professormesser.com/free-a-plus-training/220-1201/220-1201-video/network-tools-220-1201/)
- [Troubleshooting Networks — 5.5](https://www.professormesser.com/free-a-plus-training/220-1201/220-1201-video/troubleshooting-networks-220-1201/)

**Date:** 2026-05-02

---

## 概要

ネットワークの問題を診断するためのコマンドラインツールと、体系的なトラブルシューティング手順を理解する。

---

## 1. ipconfig

**用途:** 自分のデバイスのIP設定を確認する（Windows）

### 基本コマンド

| コマンド | 機能 |
|---------|------|
| `ipconfig` | IP、サブネット、ゲートウェイを表示 |
| `ipconfig /all` | 上記＋DNS、DHCP、MACアドレス等すべて表示 |
| `ipconfig /release` | DHCPリースを解放（IPアドレスを返却） |
| `ipconfig /renew` | DHCPから新しいIPアドレスを再取得 |
| `ipconfig /flushdns` | DNSキャッシュをクリア |

### 読み方のポイント
- `192.168.x.x` / `10.x.x.x` / `172.16-31.x.x` → 正常なプライベートIP
- `169.254.x.x` → APIPA = **DHCPサーバーの問題**
- DNS Serverの行が空 → **DNS設定の問題**（名前解決不可）
- Default Gatewayが空 → **ルーターに到達できない**

---

## 2. ping

**用途:** 相手デバイスに到達できるか確認する（ICMPプロトコル）

### 基本コマンド

| コマンド | 目的 |
|---------|------|
| `ping 127.0.0.1` | ローカルIPスタックの動作確認（ループバック） |
| `ping [自分のIP]` | 自分のNICが正常か確認 |
| `ping [ゲートウェイIP]` | ルーターに到達できるか確認 |
| `ping 8.8.8.8` | 外部（Google DNS）に到達できるか確認 |
| `ping google.com` | DNS名前解決 + 外部到達の両方を確認 |

### 結果の読み方
- **Reply from...** → 正常、相手に到達できた
- **Request timed out** → 相手に到達できない or ファイアウォールでブロック
- **Destination host unreachable** → ルーティングの問題
- **TTL (Time To Live)** → パケットが通過できるホップ数の上限

---

## 3. nslookup

**用途:** DNSの名前解決ができるか確認する

### 基本コマンド
```
nslookup google.com
```

### 結果の読み方
- 正常: IPアドレスが返ってくる
- 失敗: 「DNS request timed out」等 → DNSサーバーの問題
- 使用中のDNSサーバーも表示される → 正しいDNSを使っているか確認可能

### 使いどころ
- `ping 8.8.8.8` は成功するが `ping google.com` は失敗 → DNS問題
- nslookupで確認 → DNSサーバーが応答しない = DNS設定 or DNSサーバー自体の障害

---

## 4. tracert / traceroute

**用途:** 目的地までの経路（ホップ）を表示する

### 基本コマンド
```
tracert google.com      （Windows）
traceroute google.com   （Linux / Mac）
```

### 結果の読み方
```
1    1ms    192.168.1.1      ← 自分のルーター
2    5ms    10.0.0.1         ← ISPのルーター
3    15ms   203.0.113.1      ← 中継ルーター
4    20ms   142.250.x.x      ← 目的地（Google）
```

- 各行 = 1ホップ（通過するルーター）
- 時間が急に増える箇所 → ボトルネックの可能性
- `* * *` が表示 → そのルーターがICMPを返さない or 到達不可
- 途中で止まる → その地点でルーティングの問題がある

---

## 5. netstat

**用途:** 現在の接続状況・使用中のポートを表示する

### 基本コマンド

| コマンド | 機能 |
|---------|------|
| `netstat` | 現在の接続一覧 |
| `netstat -a` | すべての接続とリスニングポート |
| `netstat -n` | IPアドレスを数字で表示（名前解決しない → 高速） |
| `netstat -b` | 各接続を使用しているアプリケーションを表示 |

### 接続状態の種類

| 状態 | 意味 |
|------|------|
| ESTABLISHED | 接続中（通信できている） |
| LISTENING | ポートが開いて接続待ち |
| TIME_WAIT | 接続終了後のクールダウン |
| CLOSE_WAIT | 相手側が切断、自分側はまだ閉じていない |

---

## 6. その他のツール

| ツール | 用途 |
|--------|------|
| `pathping` | pingとtracertの機能を組み合わせ（Windows） |
| `arp -a` | ARPテーブル表示（IP↔MACアドレスの対応表） |
| Wi-Fiアナライザー | 無線ネットワークの周波数・チャンネル・信号強度を分析 |
| スペクトラムアナライザー | 周辺の全周波数帯を分析 |
| ケーブルテスター | ケーブルの配線が正しいか確認 |
| トーンジェネレーター | ケーブルの経路を特定 |
| ポートミラー（SPAN） | スイッチのトラフィックをコピーして分析 |

---

## ★ トラブルシューティング手順（体系的アプローチ）

ネットワーク問題に直面したとき、この順番で確認する：

```
ステップ1: リンクライト確認
  → LANケーブルが正しく接続されているか？（物理層）

ステップ2: ping 127.0.0.1（ループバック）
  → 自分のIPスタックは動いているか？

ステップ3: ipconfig で IP確認
  → 169.254.x.x ならDHCP問題
  → DNS Serverが空ならDNS問題

ステップ4: ping ゲートウェイ
  → ルーターに到達できるか？

ステップ5: ping 外部IP（8.8.8.8）
  → インターネットに出られるか？

ステップ6: ping ドメイン名（google.com）
  → DNS名前解決が機能しているか？
  → 5は成功で6が失敗 → DNSの問題

ステップ7: tracert で経路確認
  → どこで止まっているか特定
```

### よくある問題パターン

| 症状 | 原因 | 確認方法 |
|------|------|---------|
| 169.254.x.x のIPが出る | DHCPサーバーに到達できない | ipconfig → /release → /renew |
| 正常なIPだがWeb不可 | DNS問題 | nslookup、ipconfig /all でDNS確認 |
| 全く通信できない | ケーブル/NIC/物理層の問題 | リンクライト確認、ケーブル交換 |
| 特定サイトのみ遅い | 経路上のボトルネック | tracert で遅延箇所を特定 |
| 接続が不安定 | ポートフラッピング | リンクライトの点滅確認、ケーブル交換 |
| 全体的に遅い | 帯域不足/古い機器 | ルーター/スイッチのアップグレード検討 |

---

## 暗記チェックリスト

- [ ] ipconfig = IP設定確認、/release & /renew でDHCPリセット
- [ ] ping 127.0.0.1 = ローカルIPスタック確認
- [ ] nslookup = DNS動作確認
- [ ] tracert = 目的地までの経路表示
- [ ] netstat = 現在の接続・ポート確認
- [ ] 169.254.x.x → DHCP問題
- [ ] ping IP成功 + ping ドメイン失敗 → DNS問題
- [ ] リンクライト → ping → ipconfig → tracert の順序
- [ ] ポートフラッピング = リンクライトの不安定 → ケーブル問題の可能性

---

## Keywords

`ipconfig` `ping` `nslookup` `tracert` `traceroute` `netstat` `pathping` `arp` `loopback` `127.0.0.1` `ICMP` `TTL` `link light` `port flapping` `latency` `SPAN` `port mirror` `cable tester` `tone generator`
