# kball3 ZMK ファームウェア

**kball3** は、Seeed Studio XIAO nRF52840 (Seeeduino XIAO BLE) と光学式トラックボールセンサー **PMW3610** ブレイクアウト基板を組み合わせた、Bluetooth LE 対応の 3 ボタン式トラックボールキーボード用 ZMK ファームウェアです。

---

## 📌 ファームウェア構築の概要

### 1. ハードウェア構成とピン割当 (`kball3.kicad_pcb` 準拠)

| 機能 | XIAO ピン | マイコン内部ピン | 役割 |
| :--- | :--- | :--- | :--- |
| **BTN1** | D1 | `P0.03` | 左クリック (`&mkp LCLK`) |
| **BTN2** | D2 | `P0.28` | 中クリック (`&mkp MCLK`) |
| **BTN3** | D3 | `P0.29` | 右クリック (`&mkp RCLK`) |
| **SCLK** | D5 | `P0.05` | PMW3610 SPI クロック |
| **SDIO** | D4 | `P0.04` | PMW3610 SPI データ (双方向 3 線式) |
| **nCS** | D7 | `P1.12` | PMW3610 チップセレクト |
| **MOTION** | D10 | `P1.15` | PMW3610 モーション割り込み (IRQ) |
| **VCC** | 3V3 | `3V3` | 電源供給 |
| **GND** | GND | `GND` | グランド |

### 2. ドライバ・機能モジュール構成
- **PMW3610 センサードライバ**: `config/west.yml` にて `badjeff/zmk-pmw3610-driver` モジュールを取り込み。
- **キー入力制御**: 3つの押しボタンを直接入力 (`zmk,kscan-gpio-direct`) として制御。
- **Bluetooth 接続最適化**: Android スマートフォンや Mac との安定接続のため、BLE 送信出力を `+8dBm` に増幅し、接続パラメータを最適化。
- **自動ビルド環境**: GitHub Actions (`.github/workflows/build.yml`) により、GitHub へのプッシュ時に自動で `zmk.uf2` を生成。

---

## 🚀 ファームウェアのビルドと書き込み方法

### 1. 自動ビルド (GitHub Actions)
1. 本リポジトリの **Actions** タブを開きます。
2. 実行されたワークフローから生成された `firmware.zip` をダウンロード・解凍して `zmk.uf2` ファイルを取得します。

### 2. XIAO nRF52840 への書き込み
1. XIAO nRF52840 を USB ケーブルで PC/Mac に接続します。
2. XIAO 基板上の **RESET ボタンを 2 回連続で素早く押し**、ブートローダーモードに入れます。
3. PC にマウントされた `XIAO-SENSE` (または `NO_NAME`) ドライブに `zmk.uf2` をドラッグ＆ドロップします。
4. 自動的に書き込みが行われ、再起動後に Bluetooth デバイス `kball3` として使用可能になります。
