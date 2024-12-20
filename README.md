[TOC]

# hackintosh-colorful-b460i

> 七彩虹 B460I CVN Forzen + Intel-i5-10400 + AMD Radeon RX560 黑苹果 EFI 制作分享



## 更新日志

### 2024-11-16
> OC 引导版本为 `1.0.2-RELEASE`, 支持系统版本为 `macOS Sequioa 15.x`

1. 升级显卡为 `AMD RX6600XT`

   ![AMDRX6600XT](https://gitee.com/anlostsheep/infinity-images/raw/master/uPic/2024/20241116/IMG_8023.jpeg)
3. 增加 `macOS 14.x` 以上驱动旧博通网卡 `kext`，升级后需使用 Open-Core Patcher 安装补丁

### 2023-05-15
> OC 引导版本为 `0.9.1-RELEASE`, 支持系统版本 `macOS Ventura 13.x`

1. 更换 `Intel` 无线网卡 `AX200` 为博通 `BCM94360CS2`
   ![无线网卡图例](https://gitee.com/anlostsheep/infinity-images/raw/master/uPic/2023/IMG_4491.jpeg)
   ![系统网卡信息](https://gitee.com/anlostsheep/infinity-images/raw/master/uPic/2023/2023-5-14%2012.49.jpeg)
3. 去除 `Intel` 无线网卡 kext

### 2023-05-08
> OC 版本为 `0.9.1-RELEASE`, 支持 macOS Ventura 13.x 以上

1. 更新主板 BIOS 至 [1007版本](https://download.colorful.cn/EnDownload/MotherBroard/2022/Intel%20400/BIOS/CVN%20B460I%20GAMING%20FROZEN%20V20/CVN%20B460I%20GAMING%20FROZEN%20V20-1007.zip), 主板默认开启 ResizeBar, `config.plist` 中调整 `ResizeAppleGpuBars` 为 `0`
2. 调整 `wifi` 驱动为 [itlwm.kext](https://github.com/OpenIntelWireless/itlwm/releases/download/v2.1.0/itlwm_v2.1.0_stable.kext.zip), 主要避免的问题为 Apple 的 IO80211 系列驱动在 intel 网卡上表现极其不稳定，且每个系统大版本更新都有可能重写协议，需搭配 [HeliPort](https://github.com/OpenIntelWireless/HeliPort/releases/download/v1.4.1/HeliPort.dmg) App 一起使用
3. 调整蓝牙驱动为 [IntelBluetoothFirmware.kext](https://openintelwireless.github.io/IntelBluetoothFirmware/FAQ.html#intelbluetoothfirmware) + [IntelBTPatcher](https://openintelwireless.github.io/IntelBluetoothFirmware/FAQ.html#intelbtpatcher) 去除 [IntelBluetoothInjector.kext](https://openintelwireless.github.io/IntelBluetoothFirmware/FAQ.html#intelbluetoothinjector), macOS Montery 12.x 版本以后蓝牙协议重写，Intel 的网卡蓝牙经常断连及出现宗卷不匹配问题(无解，想要完美只能更换免驱网卡)，可以尝试杀掉蓝牙进程让其自动重启: `sudo pkill bluetoothd`, 或直接重启电脑

### 2022-03-23

1. 增加 [CPUFriend](https://github.com/acidanthera/CPUFriend/releases) 变频，使用 [CPUFriendFriend](https://github.com/corpnewt/CPUFriendFriend) 生成最大性能变频模式(需要节能模式的同学自行生成替换即可)
2. 修正 `Msic` -> `Security` -> `SecureBootModel` 为 `j185` 

### 2022-03-21

> 适配 macOS 12.x 以上

1. 更新 `OpenCore` 引导版本为 [0.7.9-RELEASE](https://github.com/acidanthera/OpenCorePkg/releases/tag/0.7.9)
2. **更新 [itlwm](https://github.com/OpenIntelWireless/itlwm) 无线网卡驱动为 [v2.1.0_stable_Monterey](https://github.com/OpenIntelWireless/itlwm/releases/download/v2.1.0/AirportItlwm_v2.1.0_stable_Monterey.kext.zip)**（使用 BigSur 版本的同学请使用 [v2.1.0_stable_BigSur](https://github.com/OpenIntelWireless/itlwm/releases/download/v2.1.0/AirportItlwm_v2.1.0_stable_BigSur.kext.zip)）

### 2022-02-14

1. 使用外置主题 [BsxOc1](https://github.com/blackosx/BsxOc1) 并添加主板硬件背景图

### 2022-02-14

1. 更新主板 `BIOS` 为 [1006](http://colorful.cn/uploads/common/2022/01/20220119155102546520.zip) 版本
2. 更新 `OpenCore` 引导为 [0.7.8-RELEASE](https://github.com/acidanthera/OpenCorePkg/releases/download/0.7.8/OpenCore-0.7.8-RELEASE.zip)

## 2021-11-23

1. 完善初始指导文档

# 硬件配置

| CPU  | [Intel i5-10400](https://ark.intel.com/content/www/cn/zh/ark/products/199271/intel-core-i5-10400-processor-12m-cache-up-to-4-30-ghz.html?wapkw=10400) |
| :--- | :----------------------------------------------------------- |
| 主板 | [七彩虹 B460I CVN Forzen V20](http://colorful.cn/product_show.aspx?mid=84&id=833) |
| 内存 | [英睿达 3000MHz 8Gx2](https://item.jd.com/100007251677.html#crumb-wrap) |
| 硬盘 | [铠侠 RC10 1TB]()                                            |
| 显卡 | [Dataland RX560D X-Serial](http://www.dataland.com.cn/prod_view.aspx?nid=3&typeid=134&id=905) |
| 网卡 | [Intel AX200](https://ark.intel.com/content/www/cn/zh/ark/products/189347/intel-wifi-6-ax200-gig.html?wapkw=ax200) |
| 机箱 | [超频三蜂鸟1](https://item.jd.com/10035164346464.html#crumb-wrap) |

## 硬件外观

<img src="https://gitee.com/anlostsheep/infinity-images/raw/master/uPic/2022/01/27/00-35-41-IMG_2954.jpeg" alt="IMG_2954" style="zoom:70%;" />

<img src="https://gitee.com/anlostsheep/infinity-images/raw/master/uPic/2022/01/27/00-44-45-IMG_2643.jpeg" alt="IMG_2643" style="zoom:50%;" />

![appearance1](https://gitee.com/anlostsheep/infinity-images/raw/master/uPic/2022/01/27/00-47-05-appearance1.jpg)

---

## 主要功能

### 关于本机

![about-this-computer](https://gitee.com/anlostsheep/infinity-images/raw/master/uPic/2022/01/27/00-47-27-about-this-computer.png)

### CPU 睿频

<img src="https://gitee.com/anlostsheep/infinity-images/raw/master/uPic/2022/01/27/00-47-43-cpu-turbo.png" alt="cpu-turbo" style="zoom:50%;" />

### 核显加速

![egpu](https://gitee.com/anlostsheep/infinity-images/raw/master/uPic/2022/01/27/00-47-59-egpu.png)

### 千兆网卡

![ethernet](https://gitee.com/anlostsheep/infinity-images/raw/master/uPic/2022/01/27/00-48-15-ethernet.png)

### WIFI

<img src="https://gitee.com/anlostsheep/infinity-images/raw/master/uPic/2022/01/27/00-48-27-wifi.png" alt="wifi" style="zoom:50%;" />

### 蓝牙

![bluetooth](https://gitee.com/anlostsheep/infinity-images/raw/master/uPic/2022/01/27/00-48-39-bluetooth.png)

### 声卡

> ALC layoutID 为 7，平时基本不用主板的音频接口就没有音箱外接显示了

![audio](https://gitee.com/anlostsheep/infinity-images/raw/master/uPic/2022/01/27/00-48-50-audio.png)

### 独立显卡

> 实际上我使用的是迪兰 RX460 X-Serial 896 流处理器版，刷了蓝宝石 RX560 1024 流处理器的 [VBIOS](https://www.techpowerup.com/vgabios/192320/sapphire-rx560-4096-170419)，原则上只要是显存颗粒是镁光类型的 400/500 系 AMD 显卡都可以刷

![egpu](https://gitee.com/anlostsheep/infinity-images/raw/master/uPic/2022/01/27/00-49-19-egpu.png)

### USB 端口定制

> USB 的定制根据机箱的不同可能不通用，我的机箱上仅有一个 USB3.0 接口为 SS06，预留了两个 SS07 及 SS08 为机箱上有 2-3个 USB3.0 接口的机箱通用，如果所使用的机箱接口还有 USB2.0，需要取舍自己需要的接口重新定制

![usb-port](https://gitee.com/anlostsheep/infinity-images/raw/master/uPic/2022/01/27/00-49-31-usb-port.png)

### iCloud

![iCloud](https://gitee.com/anlostsheep/infinity-images/raw/master/uPic/2022/01/27/00-49-41-iCloud.png)

### iMessage

![imessage](https://gitee.com/anlostsheep/infinity-images/raw/master/uPic/2022/01/27/00-49-57-imessage.png)

### 其他无法展示的功能

| 睡眠及唤醒 | 功能正常，定制了 USB 端口以及使用 SSDT-GPRW.aml 睡眠即醒补丁 |
| ---------- | ------------------------------------------------------------ |



---

## 引导方式

> 采用 [OpenCore](https://github.com/acidanthera/OpenCorePkg) 方式引导，版本为 `0.7.5 RELEASE`

---

## 镜像

> macOS 镜像根据个人喜好获取或制作，建议选择的 macOS 镜像系统在 Bigsur 11.2.3 及以下，方便后续定制 USB 端口操作

1. 国内大佬[黑果小兵的部落阁](https://blog.daliansky.net/)获取(最新的镜像是关注小兵的微信公众号通过打赏获得分享链接下载)

   > 小兵的镜像附带 WinPE, OpenCore, Clover 三分区引导的，在调试时更方便，个人比较推荐

2. 通过 macOS 上的 App Store 制作

   > 好处是纯净，通过自己的能力制作，更容易获得成就感(更好地装13)，细致教程可以参考 [tonymacx86](https://www.tonymacx86.com/threads/unibeast-install-macos-catalina-on-any-supported-intel-based-pc.285366/#download) 的这篇以 `macOS Catalina` 为例的文章自行尝试

---

## U 盘刻录

**需要注意的点**

1. 16GB 及以上的容量(镜像+分区空间都在 12GB 左右)
2. 非杂牌 U 盘(用的黑片回收颗粒，读写速度堪忧，镜像刻录和安装系统时得等个半天)，最好大品牌
3. 使用 [balenaEtcher](https://www.balena.io/etcher/) 刻录镜像到 U 盘，好处是开源，macOS, Windows, Linux 系统通用

---

## B460I BIOS 升级(可选)

> 最新版的 `BIOS` 支持更多选项 

1. 前往 [七彩虹B460I 官网主板技术支持](http://colorful.cn/product_show.aspx?mid=84&id=833)，下载最新的 `BIOS` 文件

   ![colorful-bios-support](https://gitee.com/anlostsheep/infinity-images/raw/master/uPic/2022/01/27/00-50-49-colorful-bios-support.jpg)

  2.   下载完成后得到一个 `zip` 文件，解压后得到如下图所示文件:

       ![bios-file-unzip](https://gitee.com/anlostsheep/infinity-images/raw/master/uPic/2022/01/27/00-51-08-bios-file-unzip.png)

3. 将上一步中解压得到的文件夹放入 `FAT32` 格式的 U 盘中，然后重启进入 `BIOS`，关闭 `BIOS` 中的 `Advanced` -> `PCH Configuration` -> `ME Control` 和 `Boot` -> `BIOS Write Protect` 为下一步更新 `BIOS` 做准备，`F10` 保存重新进入 `BIOS`

4. 找到以下界面中描述的选项，`BIOS` 文件选择 U 盘中的 `bin` 文件，点击 update 升级，升级前确保机器不会被断电：

   ![bios-update-action](https://gitee.com/anlostsheep/infinity-images/raw/master/uPic/2022/01/27/00-51-17-bios-update-action.png)

4. 升级完成会自动重启，重新进入 `BIOS` 检查 `BIOS` 的版本是否已经更改为最新的

---

## `BIOS` 调节选项

>  某些选项 B460I 主板没有，可能后续升级的 `BIOS` 中有，统一列出说明



**OC 推荐关闭项**

1. Fast Boot: 快速启动

   - B460I 没有此项

2. Secure Boot: 安全启动

   - Advanced -> Boot -> Secure Boot

3. Serial/COM Port: 串行端口

   - B460I 没有此项

4. Parallel Port: 并行端口

   - B460I 没有此项

5. VT-d: 虚拟化设置(Intel Virtual Technology)

   > 个人感觉不影响安装，有虚拟化的需求的要打开

   - Advanced -> Advanced -> CPU Configuration -> Intel(VMX) Virtualization Technology 

6. CSM: 兼容性支持模块(Compatibility Support Module)

   - Advanced -> Advanced -> CSM Configuration -> Disabled

7. Thunderbolt: 雷电口

   - B460I 没有此项

8. Intel SGX: Intel 安全容器技术

   - B460I 没有此项

9. Intel Platform Trust: PTT

   > 如果需要安装 Windows11 系统需要开启

10. CFG Lock: CFG 锁

    - OC -> CFG Lock -> Disabled



**OC 推荐开启的选项**

1. VT-x: CPU的硬件虚拟化技术的一种指令集
   - B460I 没有此项
2. Above 4G decoding: 
   - B460I 没有此项
3. DVMT: 动态显存分配技术
   - Advanced -> Advanced -> PCH Configuration -> Primary Display: PEG
   - Advanced -> Advanced -> PCH Configuration -> Internal Graphic: Enabled
   - Advanced -> Advanced -> PCH Configuration -> IGFX Memory Size: 128M(或以上)
   - Advanced -> Advanced -> PCH Configuration -> DVMT Total Gfx Mem: 128M(或以上)
4. XMP: 内存超频功能
   - OC -> Memory Configuration -> Memory Profile: XMP Profile1
5. XHCI Hand-off:
   - Advanced -> Advanced -> USB Configuration -> XHCI Hand-off: Enabled
6. SATA Mode: AHCI
   - Advanced -> Advanced -> SATA Configuration -> SATA Mode Selection: AHCI

---

## 安装过程

> 略……

---

## EFI 食用方式

1. 下载 `RELEASE` 版本中的 EFI-share 文件并改名为 EFI 文件

2. 使用 [Propertree](https://github.com/corpnewt/ProperTree) 或者 [OCAT](https://github.com/ic005k/QtOpenCoreConfig) 打开 EFI/OC/config.plist 文件

3. 使用 [genSMBIOS](https://github.com/corpnewt/GenSMBIOS) 生成机器对应的三码信息放入到如下图样例所示：

   ![platform-info](https://gitee.com/anlostsheep/infinity-images/raw/master/uPic/2022/01/27/00-51-43-platform-info.png)
   
   又或者使用 OCAT 自动生成三码:![ocat-platform](https://gitee.com/anlostsheep/infinity-images/raw/master/uPic/2022/01/27/00-51-56-ocat-platform.png)

4. 放 EFI 文件放入安装 macOS 的磁盘 EFI 分区的根目录下即可

---

