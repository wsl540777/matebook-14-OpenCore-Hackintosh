# Matebook 14 2020 OpenCore Hackintosh for Tahoe 26.2

### 机型配置信息
| 项目 | 详细参数|
| :--: | :-------------------- |
| 型号 | 华为 Matebook 14 2020 (KLVC-WFE9L) |
| CPU | Intel Core i7 10510U |
| 内存 | 16 GB 2133 MHz LPDDR3 |
| GPU | Intel Comet Lake-U GT2 (UHD Graphics 620) & NVIDIA GeForce MX350 |
| 硬盘 | WD SN730 512G |
| 声卡 | Realtek ALC256 |
| 无线网卡 | Intel Wireless-AC 9560 |
| 显示屏 | 奇美 CMN8C02 (P140ZKA-BZ1) 2160*1440 |

### 支持
* CPU（支持睿频）
* Intel 核显（仿冒 UHD 630，性能更接近原生）
* 睡眠和休眠
* USB 3.0/2.0
* 触控板/触摸屏（最新修复适配）
* 无线网卡（Tahoe 下暂时只能使用 Itlwm + Heliport）
* 蓝牙
* 声卡 扬声器/麦克风/耳机（Tahoe 下需通过 OCLP-Mod 注入驱动支持，耳麦暂不支持）
### 不支持
* 摄像头（解决方案：通过 Camo Studio 连续互通）
* MX350 独显
### 未测试
* HDMI
### 使用指南
## 安装前

