# Virtualization Services — CompTIA A+ 220-1201 — 4.1

**Source:** Professor Messer  
**URL:**
- [Virtualization Concepts — 4.1](https://www.professormesser.com/free-a-plus-training/220-1201/220-1201-video/virtualization-concepts-220-1201/)
- [Virtualization Services — 4.1](https://www.professormesser.com/free-a-plus-training/220-1201/220-1201-video/virtualization-services-220-1201/)

**Date:** 2026-05-04

---

## 概要

仮想化の仕組み、ハイパーバイザーの種類、VMに必要なリソース、仮想ネットワークを理解する。

---

## 1. 仮想化（Virtualization）とは

- 1台の物理マシン上で **複数のOS** を同時に実行する技術
- 各VMは独立したCPU、メモリ、ネットワーク、ストレージを持つ
- 例: Mac上でWindows 11とLinuxを同時実行

### 仮想化の用途
- **サンドボックス** — 安全な隔離環境でテスト（マルウェア分析等）
- **ソフトウェア開発** — 異なるOS/環境でアプリをテスト
- **レガシーソフトウェア** — 古いOSでしか動かないソフトを仮想環境で実行
- **クロスプラットフォーム** — Mac上でWindowsを使う等

---

## 2. ハイパーバイザー（Hypervisor）

VMを作成・管理するソフトウェア。CPU、メモリ、ネットワーク、ストレージを各VMに割り当てる。

### Type 1 vs Type 2

| | Type 1（ベアメタル） | Type 2（ホスト型） |
|--|---------------------|-------------------|
| 動作場所 | ハードウェア上に直接 | OS上で動作 |
| 用途 | サーバー/データセンター | デスクトップ/開発・テスト |
| 例 | VMware ESXi, Microsoft Hyper-V | VirtualBox, VMware Workstation |
| パフォーマンス | 高い（OSの上に載らないため） | 低い（ホストOSのオーバーヘッド） |

```
Type 1:
[VM1] [VM2] [VM3]
  [ハイパーバイザー]
    [ハードウェア]

Type 2:
[VM1] [VM2]
  [ハイパーバイザー]
    [ホストOS（Windows等）]
      [ハードウェア]
```

---

## 3. VMに必要なリソース

### CPU
- 仮想化対応のCPUが必要
- **Intel: VT（Virtualization Technology）**
- **AMD: AMD-V**
- BIOSで有効化する必要がある場合あり

### メモリ（RAM）
- 各VMにOSごとのメモリが必要
- 例: ホストOS 8GB + VM1 4GB + VM2 4GB = 最低16GB必要
- 物理RAMが足りないとパフォーマンスが大幅に低下

### ストレージ
- 各VMにOS + アプリ + データ分のディスク容量が必要
- 1つのVMで数十GBは普通に消費する
- SSDが推奨（読み書き速度が重要）

### ネットワーク
- 各VMはネットワーク接続が必要
- **仮想スイッチ（Virtual Switch）** で管理される

---

## 4. 仮想ネットワーク / 仮想スイッチ（★今日の問題）

### 仮想スイッチとは
- VMのネットワーク接続を管理する **ソフトウェア的なスイッチ**
- 物理スイッチと同じ役割（トラフィックの転送）
- ハイパーバイザーが仮想スイッチを作成・管理する

### 仮想ネットワークの接続モード

| モード | 動作 |
|--------|------|
| ブリッジ（Bridged） | VMが物理ネットワークに直接接続。物理マシンと同じネットワーク上に見える |
| NAT | VMはホストのIPを共有して外部と通信。外部からVMには直接アクセス不可 |
| ホストオンリー | VMはホストとだけ通信可能。外部ネットワークには出られない |
| 内部ネットワーク | VM同士だけで通信。ホストや外部とは通信不可 |

### ★ VMがオフラインになる原因
- 仮想スイッチが正しく設定されていない
- ネットワークアダプターがVMに割り当てられていない
- 接続モードが適切でない（ホストオンリーだと外部に出られない等）

> **試験ポイント:** 「VMがオフライン」「ハイパーバイザーはオンライン」→ Virtual Switch の設定を確認

---

## 5. VDI（Virtual Desktop Infrastructure）

- シンクライアント（最低限のハードウェア）からサーバー上のVMにリモート接続
- アプリケーションはサーバー側で実行される
- クライアント側は画面表示・キーボード・マウスのみ
- 一元管理がしやすい（IT管理者がサーバー側でVM管理）
- ネットワーク品質が重要（遅延が大きいと操作感が悪い）

---

## 6. コンテナ（Containerization）

### VMとの違い

| | VM | コンテナ |
|--|-----|---------|
| OS | 各VMに独自のOS | ホストOSのカーネルを共有 |
| サイズ | 大きい（GB単位） | 小さい（MB単位） |
| 起動速度 | 遅い（OSの起動が必要） | 速い（OSの起動不要） |
| オーバーヘッド | 大きい | 小さい |
| 例 | VirtualBox, ESXi | Docker, Kubernetes |

- コンテナはアプリとその依存関係だけをパッケージ化
- ゲストOSが不要なので軽量・高速
- 開発環境の統一やマイクロサービスで活用

---

## 暗記チェックリスト

- [ ] ハイパーバイザー = VMを管理するソフトウェア
- [ ] Type 1 = ベアメタル（ESXi, Hyper-V）→ サーバー向け
- [ ] Type 2 = ホスト型（VirtualBox, VMware Workstation）→ デスクトップ向け
- [ ] Intel VT / AMD-V = CPU仮想化支援技術
- [ ] VMに必要: CPU + RAM + ストレージ + ネットワーク
- [ ] 仮想スイッチ = VMのネットワーク接続を管理
- [ ] VMオフライン + ハイパーバイザーはオンライン → Virtual Switch の問題
- [ ] ブリッジ = 物理ネットワークに直接接続
- [ ] NAT = ホストのIPを共有
- [ ] ホストオンリー = ホストとだけ通信
- [ ] VDI = サーバー上のVMにリモート接続
- [ ] コンテナ = OSのカーネル共有、軽量、Docker

---

## Keywords

`hypervisor` `Type 1` `Type 2` `bare metal` `ESXi` `Hyper-V` `VirtualBox` `virtual switch` `bridged` `NAT` `host-only` `Intel VT` `AMD-V` `VDI` `thin client` `container` `Docker` `sandbox` `guest OS` `host OS`
