# kernel-demo : Linux Kernel + BusyBox + Kernel Module
Minimal Linux kernel & module demo

## 一、實驗目的

本實驗的目標是從零開始建構一個最小可啟動的 Linux 系統，  
透過自行編譯 Linux Kernel、搭配 BusyBox 建立 initramfs，  
並在 QEMU 虛擬機中啟動系統，同時載入自製的 Linux Kernel Module，  
實際驗證 Kernel Module 的插入、移除與 `/proc` 介面互動。

---

## 二、實驗環境

- Host OS：Windows + VirtualBox  
- Guest OS：Ubuntu 20.04 LTS  
- Linux Kernel Version：6.6.15  
- BusyBox Version：1.36.1  
- Emulator：QEMU (x86_64)

---

## 三、專案內容說明

本 Repository 內提供完整實驗成果，已整理並打包為單一壓縮檔：kernel-demo-final.tar.gz

解壓後內容包含：

- `linux-6.6.15/`  
  Linux Kernel 原始碼與編譯結果（含 bzImage）

- `busybox-1.36.1/`  
  BusyBox 原始碼、安裝結果（_install）與 initramfs 建立檔案

- `modules/`  
  自行撰寫與編譯之 Kernel Modules：
  - `hello.c` / `hello.ko`
  - `proc_demo.c` / `proc_demo.ko`
  - `Makefile`

---

## 四、系統啟動方式（QEMU）

在解壓後的專案目錄下，執行以下指令即可啟動系統：

```bash
qemu-system-x86_64 \
  -kernel linux-6.6.15/arch/x86/boot/bzImage \
  -initrd busybox-1.36.1/initramfs.cpio.gz \
  -nographic \
  -append "console=ttyS0 rdinit=/init"

成功後即可進入 BusyBox shell 環境

