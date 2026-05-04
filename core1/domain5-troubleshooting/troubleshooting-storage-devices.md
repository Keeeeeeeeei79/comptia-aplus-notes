# Troubleshooting Storage Devices — CompTIA A+ 220-1201 — 5.2

**Source:** Professor Messer  
**URL:** [Troubleshooting Storage Devices — 5.2](https://www.professormesser.com/free-a-plus-training/220-1201/220-1201-video/troubleshooting-storage-devices-220-1201/)  
**Date:** 2026-05-04

---

## 概要

ストレージデバイス（HDD/SSD）のトラブルシューティング、RAID障害の対応、S.M.A.R.T.監視、IOPSの比較を理解する。

---

## 1. ドライブの読み書きエラー

### 症状
- 「Cannot read from the source disk」等のエラーメッセージ
- ドライブが同じ箇所を何度もリトライ → パフォーマンスが低下
- ドライブの一部分だけが影響を受けることもある（断続的に発生）

### HDDの物理的な故障

| 音 | 原因 |
|----|------|
| カチカチ（clicking） | ヘッドの故障 / プラッタの損傷 → 「Click of Death」 |
| グラインド（grinding） | 金属同士の接触 / 機械部品の摩耗 |

- HDDはプラッタが5,400RPM以上で回転
- アクチュエータアームのヘッドがプラッタ上を移動
- 非常に高い精度で動作 → 1つでも壊れるとカスケード故障になる

### ★ 異音が聞こえたらやること（最重要）
1. **即座にバックアップを取る** ← 最優先
2. ケーブルの緩み・損傷を確認（デスクトップの場合）
3. ケース内の温度を確認（過熱の可能性）
4. 最近ハードウェアを追加した → PSUの電力不足の可能性
5. メーカーの診断ツールを実行（一晩かけて全セクタ検査）

---

## 2. ドライブが認識されない

### エラーメッセージのパターン

| メッセージ | 意味 |
|-----------|------|
| Drive not recognized | ドライブ自体が検出されない |
| Boot device not found | 起動用ドライブが見つからない |
| Operating system not found | ドライブは見えるがOSが見つからない |
| アクセスライトが点かない | ドライブに一切アクセスできていない |

### チェック手順
1. 電源ケーブルとデータケーブルをリシート（抜き差し）
2. BIOSのブート順序を確認（USBから起動していないか）
3. USBフラッシュドライブが挿さっていないか確認
4. 新品ドライブの場合 → ケーブル、電源、BIOSの設定を確認
5. 別のケーブルに交換して試す
6. ドライブを別のPCに接続して問題を切り分け

### 「Operating system not found」vs「Drive not recognized」
- OS not found → ドライブは見えてる、でもOSがない → ブート設定 or OS破損
- Drive not recognized → ドライブ自体が見えない → ケーブル or ドライブ故障

---

## 3. SSDの特徴

- SSD故障時 → **書き込みはできなくなるが、読み取りはできることが多い**
- これはHDDと異なる重要な特性
- SSD故障 = データ復旧の可能性がHDDより高い場合がある

---

## 4. RAID（Redundant Array of Inexpensive Disks）

### RAIDの種類（★暗記必須）

| RAID | 名前 | 最低ドライブ数 | 冗長性 | 許容故障数 | 特徴 |
|------|------|--------------|--------|-----------|------|
| RAID 0 | ストライピング | 2 | なし | 0（1台でも壊れたら全滅） | 高速だが危険 |
| RAID 1 | ミラーリング | 2 | あり | 1台 | 完全コピー |
| RAID 5 | ストライピング+パリティ | 3 | あり | 1台 | コスパ良い |
| RAID 6 | ストライピング+2重パリティ | 4 | あり | 2台 | より安全 |
| RAID 10 | ストライピング+ミラーリング | 4 | あり | 各ミラーから1台ずつ | 高速+安全 |

### RAID障害時の対応
- RAID 0 → バックアップからの復旧のみ（冗長性なし）
- RAID 1/5/6/10 → 不良ドライブを交換 → 自動再構築（リビルド）
- RAIDコントローラーのエラーメッセージ / メール通知 / 警告音を確認
- **正しいドライブを交換すること**（同じ見た目のドライブが多いので注意）

---

## 5. S.M.A.R.T.（Self-Monitoring, Analysis, and Reporting Technology）

### 概要
- ドライブに内蔵された自己監視技術
- 稼働時間、温度、エラー率、電源サイクル数等の統計を収集
- サードパーティツールで読み取り・分析

### 活用法
- 定期的にチェック（日次/週次/月次）
- 統計が徐々に悪化 → **完全故障前にドライブを交換**できる
- RAIDコントローラーはS.M.A.R.T.の監視機能が組み込まれている場合が多い
- メール/テキスト通知を設定しておく

### 主な監視項目
- Power_On_Hours（稼働時間）
- Power_Cycle_Count（電源サイクル数）
- Temperature_Celsius（温度）
- Reallocated_Sector_Count（代替セクタ数）→ これが増えると危険

---

## 6. IOPS（Input/Output Operations Per Second）

### 概要
- ストレージの読み書き性能を示す指標

### HDD vs SSD

| | HDD | SSD |
|--|-----|-----|
| IOPS | 約200 | 約1,000,000 |
| 速度 | 遅い（機械的なアクセス） | 超高速（電子的なアクセス） |

→ **HDDをSSDに交換するだけで劇的なパフォーマンス改善**

---

## 7. ネットワークドライブの問題

### マップドライブが消える場合
- ログインスクリプトの確認
- 手動で再マッピング
- 「Reconnect at sign-in」にチェックが入っているか確認
- ネットワーク接続自体の問題も確認

---

## 8. ドライブコントローラーの障害

- 外付けRAIDコントローラーが故障する場合もある
- 起動時のメッセージでコントローラーのステータスを確認
- 「RAID exception detected」等のメッセージ → コントローラーの設定ユーティリティで調査

---

## 暗記チェックリスト

- [ ] カチカチ音 = HDD故障のサイン → まずバックアップ
- [ ] SSD故障 → 書き込み不可でも読み取りはできる場合あり
- [ ] RAID 0 = 冗長性なし、1台故障で全滅
- [ ] RAID 1 = ミラーリング、1台故障OK
- [ ] RAID 5 = パリティ、1台故障OK、最低3台
- [ ] RAID 6 = 2重パリティ、2台故障OK、最低4台
- [ ] RAID 10 = ストライプ+ミラー、各ミラーから1台ずつ故障OK
- [ ] S.M.A.R.T. = ドライブの自己監視技術
- [ ] IOPS: HDD ≈ 200 / SSD ≈ 1,000,000
- [ ] 「OS not found」→ ドライブは見えるがOSがない
- [ ] 「Drive not recognized」→ ドライブ自体が見えない
- [ ] 「FIRST」問題 → データ保全・バックアップが最優先

---

## Keywords

`clicking noise` `click of death` `grinding` `HDD failure` `SSD` `RAID 0` `RAID 1` `RAID 5` `RAID 6` `RAID 10` `striping` `mirroring` `parity` `S.M.A.R.T.` `IOPS` `boot device not found` `drive not recognized` `OS not found` `mapped drive` `RAID controller` `backup`
