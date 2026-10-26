# MiniEink · 1.54 寸墨水屏驱动板

基于 **ESP32-C3** 的 1.54 寸电子墨水屏驱动板：Type-C 供电 + 锂电池充电、RTC 掉电走时、板载温湿度与加速度传感器、MicroSD 卡槽，配套 SolidWorks 外壳（上盖 / 下盖 / 主控板）。

- 原理图与 PCB：**Altium Designer**
- 结构件：**SolidWorks**
- 屏幕：**微雪 1.54inch e-Paper V2**（24P FPC 直插）

## 硬件特性

| 模块 | 器件 | 说明 |
| --- | --- | --- |
| 主控 | ESP32-C3FH4 | RISC-V，Wi-Fi + BLE 5，QFN-32，板载 2.4G PCB 天线 |
| 显示接口 | FPC 0.5mm 24P | 适配微雪 1.54inch e-Paper V2 模块 |
| 供电 | USB-C 16P + TP4056 | 5V 输入，锂电池充电管理（ESOP8） |
| 稳压 | 1117-3.3（SOT-89） | 3.3V LDO |
| 电源开关 | MSK12C02 | 机械拨动开关 |
| RTC | BM8563 + 32.768kHz | I²C 实时时钟，掉电走时 |
| 传感器 | AHT20 / SC7A20H | 温湿度（3×3mm）/ 三轴加速度（LGA-12） |
| 存储 | MicroSD（TF） | SPI 卡槽 |
| 交互 | 3 按键 + 3 LED | BOOT/左、确认、右；红/绿状态指示 |
| 保护 | USBLC6-2SC6、SS14、MBR0530 | USB ESD 保护、防反接与续流 |

## 目录结构

```
.
├── hardware/     Altium 工程（.PrjPcb / .SchDoc / .PcbDoc / .OutJob）
├── mechanical/   SolidWorks 模型（装配体 / 上盖 / 下盖 / 主控板）
├── docs/         屏幕数据手册、元件清单 BOM
├── LICENSE       CC BY-NC-SA 4.0
└── README.md
```

## 打开方式

| 内容 | 工具 | 入口文件 |
| --- | --- | --- |
| 原理图 / PCB | Altium Designer（建议 21 及以上） | `hardware/MiniEink 1.54寸墨水屏.PrjPcb` |
| 出图 / 制造文件 | Altium Designer | `hardware/MiniEink 1.54寸墨水屏.OutJob` |
| 结构件 | SolidWorks（建议 2021 及以上） | `mechanical/装配体.SLDASM` |
| 屏幕规格 | 任意 PDF 阅读器 | `docs/1.54inch_e-paper_V2_Datasheet.pdf` |
| 元件清单 | Excel / WPS | `docs/BOM.xlsx` |

> 工程内保持原始中文文件名，以保证 Altium 与 SolidWorks 的内部引用不失效。跨平台 clone 时请确认系统使用 UTF-8 路径（Windows 建议在 `git config --global core.quotepath false` 下操作，避免中文名显示为转义码）。

## 设计说明

- 时钟与传感均为 I²C，与屏幕共用总线，RTC 使用独立 32.768kHz 晶振。
- 充电指示与状态指示分离，便于判断充电 / 满电 / 运行状态。
- 外壳为上下盖对接结构，主板通过 M2 螺丝固定在下盖，屏幕贴合上盖开窗。

## 版本记录

| 版本 | 日期 | 说明 |
| --- | --- | --- |
| v1.0 | 2026-10 | 初始归档：原理图、PCB、结构件、BOM 与数据手册 |

## 许可证

本项目采用 [CC BY-NC-SA 4.0](LICENSE) 许可协议：可自由查看、修改、非商业使用，需保留署名并以相同协议共享衍生作品。**禁止商业使用**，如需商用请联系作者。

## 免责声明

本设计为个人项目，未经量产验证。锂电池充放电、Type-C 供电与高压相关的操作请自行确认安全性，因使用本设计造成的任何损失由使用者自行承担。
