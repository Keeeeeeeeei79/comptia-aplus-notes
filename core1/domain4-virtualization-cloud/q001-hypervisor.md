# Q001: Hypervisor for Virtual Machine Provisioning

**Source:** Exam Premium - Core 1 (220-1201)
**Domain:** 4.0 Virtualization and Cloud Computing
**Date:** 2026-04-30

---

## Question

A systems administrator is configuring a server to host several virtual machines. The administrator configures the server and is ready to begin provisioning the virtual machines. Which of the following features should the administrator utilize to complete the task?

- A. Hypervisor
- B. Disk management
- C. Terminal services
- D. Device Manager
- E. Virtual LAN

---

## Answer

**A. Hypervisor** ✅

---

## Explanation

Hypervisor（ハイパーバイザー）は仮想マシン（VM）を作成・管理するためのソフトウェア。1台の物理サーバー上に複数のVMをプロビジョニング（構築・展開）するのに必要。

### Hypervisorの種類

- **Type 1（ベアメタル型）** — ハードウェア上に直接動く（VMware ESXi, Hyper-V）
- **Type 2（ホスト型）** — OS上で動く（VirtualBox, VMware Workstation）
- サーバー環境では基本的にType 1が使われる

### 不正解の理由

| 選択肢 | 理由 |
|--------|------|
| B. Disk Management | Windowsのディスク管理ツール。パーティション作成やフォーマット用 |
| C. Terminal Services | リモートデスクトップ接続のサービス。VM作成とは無関係 |
| D. Device Manager | ハードウェアデバイスのドライバ管理ツール |
| E. Virtual LAN | ネットワークを論理的に分割する技術。VMの作成機能ではない |

---

## Keywords

`hypervisor` `virtual machine` `provisioning` `Type 1` `Type 2` `ESXi` `Hyper-V` `VirtualBox`
