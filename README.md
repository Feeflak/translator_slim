# translator_slim
ZMK firmware for the Translator Slim keyboard.

## Matrix

3 rows × 6 columns (5 main columns + 1 thumb-cluster column).

|     | c1  | c2  | c3  | c4  | c5  | c6 (thumb) |
| --- | --- | --- | --- | --- | --- | ---------- |
| r1  | Q   | W   | E   | R   | T   | N1         |
| r2  | A   | S   | D   | F   | G   | N2         |
| r3  | Z   | X   | C   | V   | B   | N3         |

Hardware pinout:
- Rows: `P0.06`, `P0.08`, `P0.17`
- Columns: `P0.20`, `P0.22`, `P0.24`, `P1.00`, `P0.11`, `P1.04`
- Diode direction: `col2row`

## Build

```bash
west init -l config
west update
west build -s zmk/app -b translator_slim -- -DZMK_CONFIG=$PWD/config
```

## Debug / verify soldering

Debug logging is enabled over USB CDC ACM. After flashing:

```bash
west build -t flash
```

Then open the USB serial port (e.g. `/dev/ttyACM0`) with a serial monitor to see every matrix event as you press switches:

```bash
picocom -b 115200 /dev/ttyACM0
```

Each matrix position sends a distinct key in the default keymap so you can verify every switch and its coordinates.
