# 3. ネットワークサービス — CompTIA A+ 220-1201 — 2.3 / 2.4

**Source:** Professor Messer  
**URL:**
- [Network Services — 2.3](https://www.professormesser.com/free-a-plus-training/220-1201/220-1201-video/network-services-220-1201/)
- [DNS Configuration — 2.4](https://www.professormesser.com/free-a-plus-training/220-1201/220-1201-video/dns-configuration-220-1201/)
- [DHCP — 2.4](https://www.professormesser.com/free-a-plus-training/220-1201/220-1201-video/dhcp-220-1201/)

**Date:** 2026-05-02

---

## 概要

ネットワーク上で動いている主要なサービスの仕組みと役割を理解する。

---

## 1. DNS（Domain Name System）

ドメイン名をIPアドレスに変換するサービス。ポート: **UDP 53**

### 仕組み
- `www.google.com` → `142.250.x.x` に変換
- 分散型データベース（世界中に数千台のDNSサーバーが存在）
- 13のルートサーバークラスタ（実際は1000台以上）が土台

### DNSレコードの種類

| レコード | 役割 |
|---------|------|
| A | ドメイン名 → IPv4アドレス |
| AAAA | ドメイン名 → IPv6アドレス |
| CNAME | ドメインの別名（エイリアス） |
| MX | メールサーバーの指定 |
| TXT | テキスト情報（SPF, DKIM, DMARC等） |

### メール関連のDNSレコード
- **SPF（Sender Policy Framework）** — どのサーバーからメールを送れるか定義
- **DKIM（DomainKeys Identified Mail）** — メールにデジタル署名を付与して送信元を証明
- **DMARC** — SPFとDKIMの結果に基づいてメールの処理方法を指定

### 試験ポイント
- DNSが止まると、IPアドレスを直接打たない限りWebサイトにアクセスできなくなる
- 冗長化（複数サーバー）が一般的
- ipconfigでDNSサーバーが表示されない → インターネット接続不可

---

## 2. DHCP（Dynamic Host Configuration Protocol）

IPアドレスを自動で割り当てるサービス。ポート: **UDP 67（サーバー）/ 68（クライアント）**

### DORA プロセス（★超重要）

```
D — Discover  クライアントがDHCPサーバーを探す（ブロードキャスト）
     src: 0.0.0.0:68 → dst: 255.255.255.255:67

O — Offer     DHCPサーバーがIPアドレスを提案（ブロードキャスト）
     src: DHCPサーバーIP:67 → dst: 255.255.255.255:68

R — Request   クライアントが提案を受け入れる（ブロードキャスト）
     src: 0.0.0.0:68 → dst: 255.255.255.255:67

A — Acknowledge  DHCPサーバーが確認・割当確定（ブロードキャスト）
     src: DHCPサーバーIP:67 → dst: 255.255.255.255:68
```

→ すべてブロードキャスト通信（クライアントはまだIPを持っていないため）

### DHCPが配布する情報
1. IPアドレス
2. サブネットマスク
3. デフォルトゲートウェイ
4. DNSサーバー
5. その他（NTPサーバー、VoIPサーバー等）

### DHCP用語

| 用語 | 意味 |
|------|------|
| スコープ | IPアドレス範囲やオプション設定の全体セット |
| プール | スコープ内の利用可能なIPアドレスの集合 |
| リース | IPアドレスの貸出期間（期限切れで返却） |
| 予約（Reservation） | 特定デバイスに常に同じIPを割り当てる設定 |
| 除外（Exclusion） | プールから除外するIPアドレス（ルーター等の固定IP用） |

### DHCPが失敗した場合
- クライアントは **APIPA** アドレス（169.254.x.x）を自動割当
- 169.254.x.x ではインターネットに接続できない
- ipconfigで169.254.x.x が見えたら → DHCPの問題

---

## 3. その他の主要サービス

| サービス | 役割 |
|---------|------|
| ファイル共有 | ファイルの一元管理・共有（Windows: SMB, Mac: AFP） |
| プリントサーバー | 印刷ジョブの管理・キュー管理（SMB, IPP, LPD） |
| メールサーバー | メールの送受信（SMTP送信、POP3/IMAP受信） |
| Syslog / SIEM | ログの一元収集・分析。セキュリティ監視に必須 |
| Webサーバー | HTTP/HTTPSでブラウザにページを提供 |
| 認証サーバー（AAA） | ユーザー認証・権限管理・アクセス記録 |
| データベースサーバー | 情報をテーブルで管理（SQL） |
| NTPサーバー | 時刻同期（暗号化やログ分析に正確な時刻が必要） |
| スパムゲートウェイ | 迷惑メールのフィルタリング |
| ロードバランサー | トラフィックを複数サーバーに分散 |
| プロキシサーバー | クライアントの代わりにリクエストを中継 |

---

## 暗記チェックリスト

- [ ] DNS = UDP 53、ドメイン名→IPアドレス変換
- [ ] DNSレコード: A, AAAA, CNAME, MX, TXT
- [ ] DHCP = UDP 67/68、IPアドレス自動割当
- [ ] DORA = Discover → Offer → Request → Acknowledge
- [ ] DHCPが配布: IP、サブネット、ゲートウェイ、DNS
- [ ] DHCP失敗 → APIPA（169.254.x.x）
- [ ] DHCP予約 = 特定デバイスに固定IPを割当
- [ ] Syslog → SIEM にログを集約
- [ ] AAA = Authentication, Authorization, Accounting
- [ ] NTP = 時刻同期

---

## Keywords

`DNS` `DHCP` `DORA` `scope` `pool` `lease` `reservation` `APIPA` `A record` `AAAA` `CNAME` `MX` `SPF` `DKIM` `DMARC` `syslog` `SIEM` `AAA` `NTP` `SMB` `proxy` `load balancer`
