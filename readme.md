# Matebook 14 2020 OpenCore Hackintosh for Tahoe 26.2

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
* 声卡 扬声器/麦克风/耳机输出（Tahoe 下需通过 OCLP-Mod 注入驱动支持，耳麦暂不支持）
* Siri
* 通行密钥
* 连续互通：接力/通用剪贴板（仅同一局域网的其它设备 -> Mac）/ 电话和短信转发
* 连续互通（有线）：随航 / 插入速绘、照片和扫描件 / 共享 Wi-Fi
### 不支持
* HDMI（原因未知，解决中）
* 摄像头（解决方案：通过 Camo Studio 连续互通）
* 指纹
* MX350 独显
* 连续互通： 隔空投送 / 通用控制 / 连续互通相机 / iPhone 镜像 / 使用 Apple Watch 解锁 Mac
* 定位服务/查找（定位服务依赖于 Wi-Fi，而 Itlwm 使用的是虚拟的以太网） 
## 使用指南（简明）
### 安装前
1. 准备至少 1 个 空 U 盘
2. 使用 [**OpenCore Auxiliary Tools \(OCAT\)**](https://github.com/ic005k/OCAuxiliaryTools) 或 [**OpenCore Configurator**](https://mackie100projects.altervista.org/category/opencore-configurator/) 向本 EFI 中注入三码（[教程](https://www.cnblogs.com/codtina/p/18314522)）；
3. 下载好 Heliport 客户端（用于连接 Wi-Fi）（[链接](https://github.com/OpenIntelWireless/HeliPort/releases)）
### 安装过程
* 从 Windows 下开始全新安装：
  * 方法一：从 U 盘使用官方 Recovery 安装（仅需一个 U 盘，无需自行下载完整系统镜像）
    1. 做好原有系统备份和 EFI 分区备份；
    2. 系统分区的准备
       1. EFI 分区扩容：制作一个 U 盘启动盘（推荐 [HotPE](https://www.hotpe.top/)，功能全，可联网），在 PE 下对电脑 EFI 分区扩容，扩容至 300MB；
       2. 使用分区工具为 macOS 系统创建分区（系统占用 20GB，完成安装至少需要 60GB，长期使用建议至少160G，酌情安排），格式化为任意分区格式均可，安装系统时会再次抹掉。
    3. 恢复分区的准备
       1. 从此处下载 Tahoe 的 Recovery Boot，解压后为一个 com.apple.recovery.boot 文件夹；
       2. U 盘创建一个 2G 大小的 FAT32 分区，复制一份准备好的的 EFI 文件夹，和com.apple.recovery.boot 文件夹一起放在该分区的根目录下；
       3. 进入 EFI > OC > Kext > itlwm.kext > Contents > Info.plist 用记事本打开，找到 WiFi_1，修改 ssid 和 password 对应的 string 值为要连接的 Wi-Fi 名称和密码，保存退出。
    4. 系统安装
       1. 重新启动，按 F2 进入 BIOS，关闭 安全启动 和 安全芯片；
       2. BIOS 中选择刚才配置的 U 盘恢复分区启动，选择黄色齿轮的 Recovery 26.0 (Portable)；
       3. 进入恢复分区后选择 磁盘工具， 将准备安装 macOS 的分区抹掉成 APFS 格式；
       4. 退出磁盘工具，选择 重新安装 macOS Tahoe；
       5. 如果能够进入安装界面且能够看到用户协议，说明上一步的网络配置是成功的。选择刚才抹掉的系统盘，按照提示安装 macOS，期间可能会多次重启；
       6. 完成初次激活，**选择不启用文件保险箱加密**；
       7. 进入 macOS， 安装 Heliport 客户端，以便后续连接 Wi-Fi。
    5. 拷贝 EFI 分区
       1. 重新启动，进入 PE 系统，将准备好的 EFI 文件夹拷贝到电脑硬盘的 EFI 分区， 使用 EasyUEFI （链接）添加引导项（[教程](https://www.bilibili.com/opus/872635104279658505)）；
       2. 重新启动，拔掉 U 盘，选择电脑硬盘中的 OpenCore 引导项，进入 macOS，安装完成。
  * 方法二：从 U 盘使用完整的系统镜像包安装（需要至少两个 U 盘，且需要自行下载 .dmg 或 .iso 格式系统镜像）
    1. 做好原有系统备份和 EFI 分区备份；
    2. 系统分区的准备
       1. EFI 分区扩容：制作一个 U 盘启动盘（推荐 [HotPE](https://www.hotpe.top/)，功能全，可联网），在 PE 下对电脑 EFI 分区扩容，扩容至 300MB；
       2. 使用分区工具为 macOS 系统创建分区（系统占用 20GB，完成安装至少需要 60GB，长期使用建议至少160G，酌情安排），格式化为任意分区格式均可，安装系统时会再次抹掉。
    3. 安装盘的准备
       1. 用另一个 U 盘制作 macOS 安装介质（[教程](https://sysin.org/blog/macos-createinstallmedia-windows/)）；
       2. 按照[这个教程](https://www.mfpud.com/topics/930/)在 文件资源管理器 挂载 EFI 分区，并将准备好的 EFI 文件夹替换进去。
    4. 系统安装
       1. 重新启动，按 F2 进入 BIOS，关闭 安全启动 和 安全芯片；
       2. BIOS 中选择刚才配置的 U 盘安装盘启动，选择黄色的 Install macOS Tahoe；
       3. 进入安装盘后选择 磁盘工具， 将准备安装 macOS 的分区抹掉成 APFS 格式；
       4. 退出磁盘工具，选择 安装 macOS Tahoe；
       5. 选择刚才抹掉的系统盘，按照提示安装 macOS，期间可能会多次重启；
       6. 完成初次激活，**选择不启用文件保险箱加密**；
       7. 进入 macOS， 安装 Heliport 客户端，以便后续连接 Wi-Fi。
    5. 拷贝 EFI 分区
       1. 重新启动，进入 PE 系统，将准备好的 EFI 文件夹拷贝到电脑硬盘的 EFI 分区， 使用 EasyUEFI （链接）添加引导项（[教程](https://www.bilibili.com/opus/872635104279658505)）；
       2. 重新启动，拔掉 U 盘，选择电脑硬盘中的 OpenCore 引导项，进入 macOS，安装完成。
* 从原有 macOS 安装：
  1. 备份原有 EFI；
  2. 替换新 EFI；
  3. 执行 Reset NVRAM 以应用变更，在 Windows 或 WinPE 下使用 EasyUEFI （链接）重新添加引导项（[教程](https://www.bilibili.com/opus/872635104279658505)）；
  4. 启动 macOS，安装 Heliport 客户端，连接网络；
  5. 使用镜像安装（推荐使用 [Mist](https://github.com/ninxsoft/Mist)）或 OTA 更新到 macOS Tahoe。
### 安装后
1. 更改键盘按键映射：系统设置 > 键盘 > 键盘快捷键 > 修饰键；
2. 更改触控板点按方式： 系统设置 > 触控板 > 光标与点按，调整为自己熟悉的点按方式；
3. 开启 HiDPI（[教程](https://zhuanlan.zhihu.com/p/205279615)， 不用操作 SIP 开关，后续注入声卡驱动需要）。目前硬件支持的最佳分辨率为 1335x890，其他分辨率可以自行设置，不支持的分辨率可能导致花屏；
4. 解决声卡问题
   1. 下载 [OCLP-Mod.pkg](https://github.com/laobamac/OCLP-Mod/releases) 并安装，按照提示 安装驱动补丁；
   2. 重启后电脑扬声器/麦克风/耳机输出应该正常工作。
5. 修复耳机电流声
   1. 下载 [ComboJack.zip](https://github.com/hoaug-tran/ComboJack/releases)，打开终端，将解压后 ComboJack_Installer 目录下的 install.sh 拖到终端中，回车运行；
   2. 重启后耳机电流声问题应该修复。
6. 启动时不自动挂载非 macOS 分区（[教程](https://apple.stackexchange.com/questions/310574/how-to-prevent-auto-mounting-of-a-volume-in-macos-high-sierra)），如果不清楚文件系统名称，可用 auto 代替；
7. 推荐工具
   * [Camo Studio](https://camo.com/studio)，将 安卓/iOS 设备摄像头用作 Mac 摄像头，实现类似连续互通相机功能；
   * [LocalSend](https://www.bing.com/ck/a?!&&p=071b07c0a213d15d01f485f1873f9f4eb1e03fd7c491c81370157bf3dfb77b97JmltdHM9MTc2NTIzODQwMA&ptn=3&ver=2&hsh=4&fclid=2ddf5985-b285-6f5c-3f28-4a49b3e36e60&u=a1aHR0cHM6Ly9hcHBzLmFwcGxlLmNvbS91cy9hcHAvbG9jYWxzZW5kL2lkMTY2MTczMzIyOQ)，替代隔空投送的局域网互传工具；
   * [Paragon NTFS for Mac](https://support-en.wd.com/app/answers/detailweb/a_id/34871)，macOS 下支持 NTFS 读写；
   * [DockDoor](https://dockdoor.net/)，窗口预览切换增强工具；
   * [Magnet](https://www.bing.com/ck/a?!&&p=acd5a40071bf838add2a885c3c612a83d70fbda9a143bf6b1b9f7fbc655cb945JmltdHM9MTc2NTIzODQwMA&ptn=3&ver=2&hsh=4&fclid=2ddf5985-b285-6f5c-3f28-4a49b3e36e60&u=a1aHR0cHM6Ly9hcHBzLmFwcGxlLmNvbS91cy9hcHAvbWFnbmV0L2lkNDQxMjU4NzY2P210PTEy)，窗口快速布局工具；
   * [Bartender](https://www.macbartender.com/)，菜单栏图标管理工具；
   * [KeyClu](https://github.com/Anze/KeyCluCask/)，学习并熟悉 macOS 快捷键功能；
   * [UninstallPKG](https://www.corecode.io/uninstallpkg/)，卸载 .pkg 安装的程序；
   * [BuhoLaunchpad](https://www.drbuho.com/buholaunchpad)，使用旧版启动台；
   * [Displaperture](https://www.bing.com/ck/a?!&&p=3c69c1b52fabfbf7f8b4649b03859b9f73110d22d617b2431f505e5346824a96JmltdHM9MTc2NTIzODQwMA&ptn=3&ver=2&hsh=4&fclid=2ddf5985-b285-6f5c-3f28-4a49b3e36e60&u=a1aHR0cHM6Ly9hcHBzLmFwcGxlLmNvbS91cy9hcHAvZGlzcGxhcGVydHVyZS9pZDE1NDM5MjAzNjI_bXQ9MTI)，让 Mac 变成圆角屏幕。
   
