# kball3

Seeed XIAO nRF52840 / XIAO BLE を使った、独立型トラックボール + 3ボタンデバイス
`kball3` のZMKファームウェア設定です。

現時点では、リポジトリ名、デバイス名、Bluetooth表示名を `kball3` として進めます。
将来的に必要があれば、個人カスタム用リポジトリ名として `kotobo3` へのリネームも検討します。

## 現在のPCBピン割り当て

キーは行列ではなく、各GPIOからスイッチを通ってGNDへ落とす直結配線です。

```text
BTN1 -> XIAO D3 -> switch -> GND
BTN2 -> XIAO D4 -> switch -> GND
BTN3 -> XIAO D5 -> switch -> GND
```

このPCBでのマウスセンサー用FPCピン順:

```text
FPC pin 1: GND
FPC pin 2: SCLK   -> XIAO D9
FPC pin 3: SDIO   -> XIAO D8
FPC pin 4: MOTION -> XIAO D6
FPC pin 5: CS     -> XIAO D7
FPC pin 6: 3V3
```

まずは3つの直結キーと基本レイヤー構成をビルドできる状態にしています。

## 現在のキーマップ案

```text
Base:
BTN1 = Backspace
BTN2 = Left click
BTN3 = Space

Combo:
BTN1 + BTN2 = LC(SPACE)
BTN2 + BTN3 = Enter
BTN1 + BTN3 = Bluetooth layer toggle
BTN1 + BTN2 + BTN3 = Mouse/Utility layer toggle

Bluetooth layer:
BTN1 = BT_SEL 0
BTN2 = BT_SEL 1
BTN3 = Base

Mouse/Utility layer:
BTN1 = Middle click
BTN2 = Right click
BTN3 = Base
```

PAW3222センサーは、作者のZMKドライバーを使う予定です。

```text
https://github.com/sekigon-gonnoc/zmk-driver-paw3222
```

このモジュールは `config/west.yml` に追加済みで、shield Kconfig 側でも `PAW3222`
を有効化しています。

SPI overlayも有効化済みです。作者ドライバーのoverlay例では `NRF_PSEL(...)` に
nRF52840の実GPIO番号を指定する必要があるため、XIAO BLEのDピンを以下のように展開しています。

```text
MOTION -> XIAO D6 -> P1.11 -> irq-gpios
CS     -> XIAO D7 -> P1.12 -> cs-gpios
SDIO   -> XIAO D8 -> P1.13 -> SPIM_MOSI / SPIM_MISO
SCLK   -> XIAO D9 -> P1.14 -> SPIM_SCK
```

XIAO BLEとセンサー変換基板はPCB裏面配置なので、KiCad表示上の見た目ではなくネット名と
XIAOピン名を基準に確認しています。
