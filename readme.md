# # Matebook 14 2020 OpenCore Hackintosh for Tahoe 26.2

## 机型配置信息
| 项目   | 详细参数                                                         |
|:----:|--------------------------------------------------------------|
| 型号   | 华为 Matebook 14 2020 (KLVC-WFE9L)                             |
| CPU  | Intel Core i7 10510U                                         |
| 内存   | 16 GB 2133 MHz LPDDR3                                        |
| GPU  | Intel Comet Lake-U GT2 (UHD Graphics 620) & NVIDIA GeForce MX350 |
| 硬盘   | WD SN730 512G                                                |
| 声卡   | Realtek ALC256                                               |
| 无线网卡 | Intel Wireless-AC 9560                                       |
| 显示屏  | 奇美 CMN8C02 (P140ZKA-BZ1) @ 2160*1440                         |
## 适配情况
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
* HDMI（原因未知，解决中）
* 摄像头（解决方案：通过 Camo Studio 连续互通）
* 指纹
* MX350 独显
* 定位服务/查找（定位服务依赖于 Wi-Fi，而 Itlwm 使用的是虚拟的以太网） 
## 使用指南
### 安装前
1. 准备至少 1 个 U 盘
2. 使用 [**OpenCore Auxiliary Tools \(OCAT\)**](https://github.com/ic005k/OCAuxiliaryTools) 或 [**OpenCore Configurator**](https://mackie100projects.altervista.org/category/opencore-configurator/) 向本 EFI 中注入三码（[教程](https://www.cnblogs.com/codtina/p/18314522)）；
3. 下载好 Heliport 客户端（用于连接 Wi-Fi）（[链接](https://github.com/OpenIntelWireless/HeliPort/releases)）
### 安装过程
* 从 Windows 下开始全新安装：
  1. 使用分区工具为 macOS 系统创建分区（系统占用 20GB，完成安装至少需要 60GB，长期使用建议至少160G，酌情安排），格式化为任意分区格式均可，安装系统时会再次抹掉；
  方法一：从 U 盘使用官方 Recovery 安装（简单，无需下载完整系统镜像）
  2. 从此处下载 Sequoia 的 Recovery Boot
  3. 用准备的 U 盘制作 macOS 安装介质（[教程](https://sysin.org/blog/macos-createinstallmedia-windows/)）；
* 从原有 macOS 安装：
  1. 备份原有 EFI；
  2. 替换新 EFI；
  3. 执行 Reset NVRAM，在 Windows 或 WinPE 下使用 EasyUEFI （链接）重新添加引导项（[教程](https://www.bilibili.com/opus/872635104279658505)）；
  4. 启动 macOS，安装 Heliport 客户端，连接网络；
  5. 使用镜像安装（推荐使用 [Mist](https://github.com/ninxsoft/Mist)）或 OTA 更新到 macOS Tahoe。
### 安装后
1. 解决花屏问题：注入EDID（教程）* MX350 独显
### 未测试
* HDMI
### 使用指南
## 安装前

