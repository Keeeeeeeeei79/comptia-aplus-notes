# CompTIA A+ IT用語集（英日対応）

**Date:** 2026-05-04（随時更新）

これまでの勉強で出てきたIT用語をカテゴリ別にまとめ。分からない単語が出てきたらここに追加していく。

---

## ネットワーク基礎

| 英語 | 読み方 | 意味 |
|------|--------|------|
| IP (Internet Protocol) | アイピー | ネットワーク上の住所。データの宛先を決める |
| TCP (Transmission Control Protocol) | ティーシーピー | 信頼性あり通信。届いたか確認する（電話的） |
| UDP (User Datagram Protocol) | ユーディーピー | 信頼性なし通信。確認しない、でも速い（郵便的） |
| DNS (Domain Name System) | ディーエヌエス | ドメイン名（google.com）→ IPアドレスに変換 |
| DHCP (Dynamic Host Configuration Protocol) | ディーエイチシーピー | IPアドレスを自動で配布する仕組み |
| NAT (Network Address Translation) | ナット | プライベートIP → パブリックIPに変換してインターネットに出る |
| APIPA | アピパ | DHCP失敗時に自動割当される仮IP（169.254.x.x） |
| Subnet Mask | サブネットマスク | どのネットワークに属するか判定する番号（例: 255.255.255.0） |
| Default Gateway | デフォルトゲートウェイ | 別のネットワークへの出口（通常はルーターのIP） |
| VLAN (Virtual LAN) | ブイラン | ネットワークを論理的に分割する技術 |
| VPN (Virtual Private Network) | ブイピーエヌ | 暗号化されたトンネルで安全にリモート接続 |
| MAC Address | マックアドレス | ネットワーク機器の固有ID（物理アドレス） |
| ICMP | アイシーエムピー | pingで使われるプロトコル。到達確認用 |
| NIC (Network Interface Card) | ニック | ネットワーク接続用のハードウェア |
| PoE (Power over Ethernet) | ピーオーイー | LANケーブルで電源も供給する技術 |

### ネットワークの種類（規模別）

| 英語 | 読み方 | 範囲 | 例 |
|------|--------|------|-----|
| PAN (Personal Area Network) | パン | 数メートル（身の回り） | Bluetoothイヤホン、スマートウォッチ |
| LAN (Local Area Network) | ラン | 1つの建物内 | オフィス内のPC、プリンター接続 |
| WLAN (Wireless LAN) | ダブルラン | 1つの建物内（無線） | Wi-Fiネットワーク |
| MAN (Metropolitan Area Network) | マン | 1つの都市内 | 市内の複数オフィスを接続 |
| WAN (Wide Area Network) | ワン | 都市間・国をまたぐ | 本社↔海外支社、インターネット |
| SAN (Storage Area Network) | サン | データセンター内 | サーバー↔ストレージ専用の高速接続 |

```
小 ←─────────────────────────→ 大
PAN → LAN → WLAN → MAN → WAN
身の回り  建物内   無線    都市内   都市間
```

---

## ネットワークデバイス

| 英語 | 読み方 | 意味 |
|------|--------|------|
| Router | ルーター | 異なるネットワーク間でデータを転送（Layer 3、IPアドレスで判断） |
| Switch | スイッチ | 同じネットワーク内のデバイスを接続（Layer 2、MACアドレスで判断） |
| Access Point (AP) | アクセスポイント | 有線ネットワークを無線に拡張するデバイス |
| Firewall | ファイアウォール | ネットワークトラフィックをフィルタリング（許可/拒否） |
| NGFW (Next-Gen Firewall) | 次世代ファイアウォール | アプリケーションレベルで判断する高機能ファイアウォール |
| Modem | モデム | アナログ↔デジタル変換。ISPとの接続に使う |
| ONT (Optical Network Terminal) | オーエヌティー | 光ファイバー↔Ethernetの変換装置 |
| Patch Panel | パッチパネル | ケーブル管理の整理用。サーバールームで使う |
| Proxy Server | プロキシサーバー | クライアントの代わりにリクエストを中継する |
| Load Balancer | ロードバランサー | トラフィックを複数サーバーに分散する |

---

## ポート & プロトコル

| 英語 | ポート | 意味 |
|------|--------|------|
| FTP (File Transfer Protocol) | 20/21 | ファイル転送（暗号化なし） |
| SSH (Secure Shell) | 22 | 暗号化されたリモート接続 |
| SFTP | 22 | SSH上のセキュアなファイル転送 |
| Telnet | 23 | リモート接続（暗号化なし、危険） |
| SMTP | 25/587 | メール送信。587はセキュア版 |
| DNS | 53 | ドメイン名→IP変換 |
| DHCP | 67/68 | IPアドレス自動配布 |
| HTTP | 80 | Web通信（暗号化なし） |
| HTTPS | 443 | Web通信（暗号化あり） |
| POP3 / POP3S | 110/995 | メール受信（ダウンロード型） |
| IMAP / IMAPS | 143/993 | メール受信（同期型、複数端末対応） |
| LDAP / LDAPS | 389/636 | ディレクトリサービス（Active Directory等） |
| SMB | 445 | Windowsファイル共有 |
| RDP (Remote Desktop Protocol) | 3389 | Windowsリモートデスクトップ |

---

## ストレージ

| 英語 | 読み方 | 意味 |
|------|--------|------|
| HDD (Hard Disk Drive) | エイチディーディー | 回転するプラッタにデータ保存。安い、大容量、遅い |
| SSD (Solid State Drive) | エスエスディー | 電子的にデータ保存。速い、耐衝撃、高い |
| NVMe | エヌブイエムイー | SSDの高速接続規格。M.2スロットに差す |
| SATA | サタ | HDD/SSDの接続規格。NVMeより遅い |
| IOPS | アイオプス | 1秒あたりの読み書き回数。HDD≈200、SSD≈1,000,000 |
| NAS (Network Attached Storage) | ナス | ネットワーク接続の共有ストレージ |
| RAID | レイド | 複数ドライブでデータを守る/速くする仕組み |
| S.M.A.R.T. | スマート | ドライブの自己監視技術。故障を予測できる |

### RAID の種類（★暗記必須）

| RAID | 名前 | 最低台数 | 壊れてOKな台数 | 特徴 |
|------|------|---------|---------------|------|
| RAID 0 | ストライピング | 2台 | 0台（1台でも壊れたら全滅） | 速い、でも危険。データ分散するだけ |
| RAID 1 | ミラーリング | 2台 | 1台 | 完全コピー。安全だが容量半分 |
| RAID 5 | ストライピング+パリティ | 3台 | 1台 | コスパ良い。パリティで復旧可能 |
| RAID 6 | ストライピング+2重パリティ | 4台 | 2台 | RAID 5より安全 |
| RAID 10 | ストライピング+ミラーリング | 4台 | 各ミラーから1台ずつ | 速い+安全。コスト高い |

### RAID を簡単に言うと

```
RAID 0 = 2冊のノートに交互に書く → 1冊なくしたら全部ダメ
RAID 1 = 同じ内容を2冊に書く → 1冊なくしてもOK
RAID 5 = 3冊以上に分散して書く + 復元用メモ付き → 1冊なくしても復元できる
```

---

## 電源

| 英語 | 読み方 | 意味 |
|------|--------|------|
| PSU (Power Supply Unit) | ピーエスユー | 電源ユニット。AC→DC変換してPCに電力供給 |
| AC (Alternating Current) | エーシー | 交流。コンセントからの電気 |
| DC (Direct Current) | ディーシー | 直流。PC内部の電気 |
| Watt (W) | ワット | 電力の単位。W = V × A |
| Volt (V) | ボルト | 電圧（電気の圧力） |
| Amp (A) | アンペア | 電流（電気の流れの量） |
| 80 PLUS | エイティプラス | PSUの電源効率認証（Bronze/Silver/Gold/Platinum/Titanium） |
| Redundant Power | 冗長電源 | PSUが2台。1台壊れても動く。サーバー向け |

### PSUが供給する電圧

| 電圧 | 用途 |
|------|------|
| +3.3V | RAM、M.2 |
| +5V | USB、一部マザーボード部品 |
| +12V | GPU、HDD、PCIe（最重要） |

---

## 起動 & BIOS

| 英語 | 読み方 | 意味 |
|------|--------|------|
| POST (Power On Self Test) | ポスト | 起動時のハードウェア自動チェック |
| BIOS (Basic Input/Output System) | バイオス | ハードウェアの基本設定を管理するファームウェア |
| UEFI | ユーイーエフアイ | BIOSの後継。GUIで操作できる |
| CMOS Battery | シーモス | BIOSの設定と時刻を保持する電池（CR2032） |
| Beep Code | ビープコード | POST失敗時のビープ音。メーカーごとに異なる |
| BSoD (Blue Screen of Death) | ブルースクリーン | Windows回復不能エラー画面 |
| Boot Sequence | ブートシーケンス | OSを起動する順番（SSD > USB等） |
| Safe Mode | セーフモード | 最小限のドライバーでWindowsを起動する診断モード |

---

## 仮想化 & クラウド

| 英語 | 読み方 | 意味 |
|------|--------|------|
| VM (Virtual Machine) | ブイエム | 仮想マシン。1台のPC上でOSを複数同時実行 |
| Hypervisor | ハイパーバイザー | VMを管理するソフトウェア |
| Type 1 (Bare Metal) | ベアメタル | ハードウェア上に直接動くハイパーバイザー（ESXi, Hyper-V） |
| Type 2 (Hosted) | ホスト型 | OS上で動くハイパーバイザー（VirtualBox, VMware Workstation） |
| Virtual Switch | 仮想スイッチ | VMのネットワーク接続を管理するソフトウェア的スイッチ |
| VDI (Virtual Desktop Infrastructure) | ブイディーアイ | サーバー上のデスクトップにリモート接続 |
| Container | コンテナ | OSカーネルを共有する軽量な仮想化（Docker） |
| Dual Boot | デュアルブート | 2つのOSを入れて起動時に選ぶ。同時使用不可 |
| Sandbox | サンドボックス | 隔離された安全なテスト環境 |
| IaaS | イアース | Infrastructure as a Service（インフラをクラウドで提供） |
| SaaS | サース | Software as a Service（ソフトをクラウドで提供） |
| PaaS | パース | Platform as a Service（開発環境をクラウドで提供） |

---

## ハードウェア

| 英語 | 読み方 | 意味 |
|------|--------|------|
| CPU (Central Processing Unit) | シーピーユー | プロセッサ。PCの脳 |
| GPU (Graphics Processing Unit) | ジーピーユー | グラフィック処理専用のプロセッサ |
| RAM (Random Access Memory) | ラム | 一時記憶メモリ。電源切ると消える |
| DDR4 / DDR5 | ディーディーアール | RAMの世代。DDR5が最新、DDR2は古すぎ |
| Motherboard | マザーボード | 全パーツを繋ぐ基板 |
| Heatsink | ヒートシンク | CPUの熱を放散する金属パーツ |
| Thermal Paste | サーマルペースト | CPUとヒートシンクの間に塗る熱伝導材 |
| ESD (Electrostatic Discharge) | 静電気放電 | 静電気でパーツが壊れる。ESDストラップで防ぐ |

---

## ファイルシステム

| 英語 | 対応OS | 特徴 |
|------|--------|------|
| NTFS | Windows | 現行主流。セキュリティ・暗号化対応 |
| FAT32 | 全OS | 古い。4GB以上のファイル不可。USBに多い |
| exFAT | 全OS | FAT32の後継。大容量ファイル対応。USB/SDカード向け |
| ext4 | Linux | Linux現行主流 |
| ext3 | Linux | 古いLinuxファイルシステム |
| APFS | macOS | Apple現行主流 |
| HFS+ | macOS | 古いAppleファイルシステム |

---

## モバイル & ラップトップ

| 英語 | 読み方 | 意味 |
|------|--------|------|
| LCI (Liquid Contact Indicator) | エルシーアイ | 液体接触インジケーター。水没確認用 |
| Desiccant | デシカント | 乾燥剤。液体損傷時に使う（米ではなくこれ） |
| Digitizer | デジタイザー | タッチスクリーンの入力を検知する層 |
| Cursor Drift / Ghost Touch | カーソルドリフト | 触ってないのに画面が勝手に反応 |
| LCD Inverter | インバーター | バックライトの電力を管理する部品 |
| Docking Station | ドッキングステーション | ラップトップに周辺機器をまとめて接続する装置 |

---

## トラブルシューティングコマンド

| コマンド | 用途 |
|---------|------|
| `ipconfig` | 自分のIP設定を確認 |
| `ipconfig /release` | DHCPリースを解放 |
| `ipconfig /renew` | DHCPから再取得 |
| `ipconfig /flushdns` | DNSキャッシュをクリア |
| `ping` | 相手に到達できるか確認 |
| `ping 127.0.0.1` | ローカルIPスタックの確認（ループバック） |
| `nslookup` | DNS名前解決の確認 |
| `tracert` | 目的地までの経路を表示 |
| `netstat` | 現在の接続・ポートを表示 |
| `arp -a` | IP↔MACアドレスの対応表を表示 |

---

## 用途別PCスペック

| 用途 | 重要パーツ |
|------|-----------|
| CAD/CAM | SSD + ハイエンドGPU + 最大RAM |
| 動画編集 | SSD + GPU + デュアルモニター + サウンドカード |
| 仮想化 | マルチコアCPU + 最大RAM |
| ゲーミング | SSD + GPU + サウンド + 冷却 |
| NAS | 大容量HDD + RAID + ギガビットNIC |
| シッククライアント | アプリ要件を満たすフルスペック |
| シンクライアント | 最低限スペック + ネットワーク品質重要 |

---

## セキュリティ用語（基礎）

| 英語 | 読み方 | 意味 |
|------|--------|------|
| AAA | トリプルエー | Authentication（認証）、Authorization（権限）、Accounting（記録） |
| SPF | エスピーエフ | メール送信元のサーバーを検証 |
| DKIM | ディーキム | メールにデジタル署名をつけて送信元を証明 |
| DMARC | ディーマーク | SPF+DKIMの結果に基づくメール処理ルール |
| Syslog | シスログ | ログの一元収集サービス |
| SIEM | シーム | セキュリティログの分析・監視システム |
| 2FA (Two-Factor Authentication) | 二要素認証 | パスワード＋もう1つ（SMS、アプリ等）で認証 |
| DMZ (Demilitarized Zone) | ディーエムゼット | メインネットワークから隔離された中間ゾーン |

---

## IoT（Internet of Things）

| 英語 | 読み方 | 意味 |
|------|--------|------|
| IoT (Internet of Things) | アイオーティー | インターネットに繋がる日常のデバイス（スマート家電等） |
| Smart Thermostat | スマートサーモスタット | Wi-Fiでスマホから操作できる温度調整器 |
| Smart Speaker | スマートスピーカー | 音声操作デバイス（Alexa, Google Home等） |
| Smart Lock | スマートロック | スマホで施錠・解錠できる鍵 |
| Firmware | ファームウェア | デバイス内蔵のソフトウェア。更新で脆弱性を修正 |

### IoTセキュリティの鉄則

| 対策 | 理由 |
|------|------|
| ネットワーク分離（DMZ/VLAN/ゲストネットワーク） | ハッキングされても他のデバイスに影響しない |
| 強い暗号化 + 強いパスワード（WPA3推奨） | 不正アクセスを防ぐ |
| デフォルトパスワードを必ず変更 | 初期パスワードは公開情報で簡単に見つかる |
| ファームウェアを最新に保つ | 脆弱性の修正 |
| 二要素認証（使えるなら） | パスワード漏洩時の保険 |

### IoTがセキュリティ的に弱い理由
- ファームウェア更新が少ない
- 処理能力が低く、強い暗号化ができない場合がある
- デフォルトパスワードが変更されないことが多い
- 大量のデバイスが常時ネットワークに接続されている

---

## Wi-Fi暗号化規格

| 規格 | 状態 | 説明 |
|------|------|------|
| WEP | ❌ 古い・危険 | 簡単に破られる。使ってはいけない |
| WPA | ❌ 古い | WEPより良いが脆弱性あり |
| WPA2 | ✅ まだ使える | AES暗号化。現在も広く使われている |
| WPA3 | ✅ 最新・最強 | 最も安全。新しいデバイスで推奨 |

> **試験ポイント:** 「WPAにアップグレード」は引っかけ。WPAは古い規格なのでダウングレードになる。

---

> **使い方:** 新しい用語が出てきたらここに追加していく。Ankiのフラッシュカードにも転記すると暗記しやすい。
