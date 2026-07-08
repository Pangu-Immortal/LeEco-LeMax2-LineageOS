<div align="center">

<img src="https://capsule-render.vercel.app/api?type=waving&color=0:a8c0ff,100:3f2b96&height=150&section=header&text=LeEco%20Le%20Max%202%20%C2%B7%20LineageOS&fontSize=40&fontColor=ffffff&animation=fadeIn&desc=A%202016%20flagship%20abandoned%20at%20Android%206%2C%20rebuilt%20from%20source%20to%20Android%2011&descSize=14&descAlignY=58" alt="header"/>

<img src="https://readme-typing-svg.demolab.com?font=Fira+Code&weight=600&size=18&pause=1000&color=6C7A96&center=true&vCenter=true&width=680&lines=Snapdragon+820+%C2%B7+abandoned+at+Android+6.0.1;Rebuilt+from+LineageOS+source+to+Android+11;Real+device+verified+%C2%B7+no+overclaiming" alt="typing"/>

<br/>

<img src="https://count.getloli.com/get/@LeEco-LeMax2-LineageOS?theme=moebooru" alt="visitors"/>

<br/><br/>

<img src="https://img.shields.io/badge/License-Apache--2.0-607D8B?style=flat-square" alt="license"/>
<img src="https://img.shields.io/badge/LineageOS-18.1-5C6BC0?style=flat-square" alt="los"/>
<img src="https://img.shields.io/badge/Android-11-26A69A?style=flat-square" alt="android"/>
<img src="https://img.shields.io/badge/Device-Le%20Max%202%20%C2%B7%20x2%20%C2%B7%20LEX820-78909C?style=flat-square" alt="device"/>
<img src="https://img.shields.io/badge/SoC-Snapdragon%20820%20%C2%B7%20MSM8996-8B7EC8?style=flat-square" alt="soc"/>
<img src="https://img.shields.io/github/stars/Pangu-Immortal/LeEco-LeMax2-LineageOS?style=flat-square&color=607D8B" alt="stars"/>

<br/><br/>

**如果对你有帮助,点个 Star ⭐ 支持一下 · If it helps, a Star means a lot**

简体中文 | [English](README_EN.md)

</div>

---

## TL;DR

**LeEco-LeMax2-LineageOS** 是 **乐视 Le Max 2(x2 / LEX820,骁龙 820 / MSM8996)** 的 **LineageOS 18.1(Android 11)源码移植统一入口**。这台 2016 年的旗舰被官方止步在 **Android 6.0.1** 后停更弃维八年,本项目从 **LineageOS 源码树**重建设备树、平台 common、内核与 vendor blobs,**跨越 5 个大版本**,让它在**真机上稳定跑通 Android 11**——`sys.boot_completed=1`、正确识别 LEX820、双卡已启用,一切结论均可用 `build.prop` 复核。怎么用:`repo init lineage-18.1` → 拉入本项目 local_manifests → `brunch x2` 出包 → recovery 侧载刷入。适用场景:老旗舰救砖复活、msm8996 自定义 ROM 学习、LineageOS 构建踩坑参考。**诚实红线:真机稳定版本 = Android 11;Android 16 仅为路线图探索,未交付即不宣称。**

---

## 目录

- [一台旗舰的死与生](#一台旗舰的死与生)
- [真机验证的事实](#真机验证的事实)
- [为什么这台机器难搞](#为什么这台机器难搞)
- [征服的坑 · 工程档案](#征服的坑--工程档案)
- [组件仓库索引](#组件仓库索引)
- [从源码构建](#从源码构建)
- [刷机指南](#刷机指南)
- [路线图](#路线图)
- [关于作者](#关于作者)

---

## 一台旗舰的死与生

> 有些设备不该被时代淘汰,它们只是被停止了维护。

| 时间线 | 状态 | 发生了什么 |
| :--- | :--- | :--- |
| **2016 · 巅峰** | 🏆 旗舰 | 骁龙 820、2K 屏、金属机身——那一年的顶级性能 |
| **2016 年底 · 停摆** | ⛔ 停更 | 官方推送最后一版 **Android 6.0.1** 后永久沉默 |
| **此后 8 年 · 遗忘** | 🪦 被弃 | 系统冻结在 Android 6,被安全更新、被生态、被时代抛下 |
| **今天 · 重生** | 🌱 复活 | 从 LineageOS **源码级重建**,真机点亮 **Android 11(LineageOS 18.1)** |

设备树、平台 common、内核、vendor blobs 全部自持维护,跨越 **5 个大版本**,把这台八年前的旗舰真机拉到现代 Android。

`Android 6.0.1` ⛔ ⟶ `7` ⟶ `8` ⟶ `9` ⟶ `10` ⟶ **`Android 11`** ✅ · `Android 16 🧭 路线图探索中`

---

## 真机验证的事实

诚实是硬核工程的底线。以下每一项都在真机上跑通、可复现:

| 验证项 | 结果 | 证据来源 |
| :-- | :-: | :-- |
| 系统启动 | ✅ `sys.boot_completed = 1` | `adb shell getprop` |
| 进入桌面 | ✅ Launcher 正常,可交互 | 真机 |
| Android 版本 | ✅ **Android 11**(`ro.build.version.release = 11`) | `build.prop` 可查 |
| 机型识别 | ✅ 正确识别 **LEX820**(源码级修复) | `ro.product.model` |
| 双卡配置 | ✅ 双卡模式已启用(dsds) | `persist.radio.multisim.config` |
| 基带 / 射频 | ✅ 基带固件已加载在线 | `gsm.version.baseband` |
| 通话/数据/WiFi/蓝牙/相机 | 🔧 未插卡逐项实测,待验证 | 以真机为准 |
| Android 16 | 🧭 路线图探索中(Treble GSI),**尚未交付** | — |

> 🧭 **不吹牛红线:** 本 ROM 真机稳定运行的版本是 **Android 11 / LineageOS 18.1**。Android 16 仅为持续推进的技术路线,**未交付即不宣称**。只写能被真机验证的东西。

---

## 为什么这台机器难搞

不是「下个源码点一下编译」就能成的活:

- **官方零支持**:LeEco 已解散,没有维护中的内核、没有新版 blobs、没有官方设备树,一切从零重建。
- **闭源 blobs 断代**:msm8996 平台大量私有二进制停留在旧 vendor,向上适配全靠人肉对齐 HAL 与 SEPolicy。
- **多变体地雷**:Le Max 2 含 `x820 / x821 / x829` 多个子型号,基带、分区、校验各不相同,认错一个就砖。
- **现代工具链断链**:用 2024/2025 的主机去编 2020 的 LOS 18.1,host 侧一路踩雷。

---

## 征服的坑 · 工程档案

| 坑 | 症状 | 根因 | 征服方式 |
| :-- | :-- | :-- | :-- |
| **ncurses5 断链** | 现代 Ubuntu 上老 clang 启动即崩 | LOS 18.1 预编译 clang 依赖已弃用的 `libncurses.so.5` | 建 `.so.6 → .so.5` 兼容软链,恢复整棵 host 工具链 |
| **webview LFS 指针** | 编译到 99% 卡死在 `webview.apk` | `repo sync` 未带 `--git-lfs`,webview.apk 只检出 LFS 指针而非真身 | 单独 clone 对应仓库并 `git lfs pull` 拉真实镜像 |
| **mke2fs orphan_file** | ART APEX / system 镜像生成失败 | 新版 e2fsprogs 的 `mke2fs.conf` 含老工具不识的 `orphan_file` 特性 | 从 `/etc/mke2fs.conf` 移除 `orphan_file` |
| **/data bootloop** | 首刷卡开机动画、`credstore` 崩溃循环 | `fastboot erase` 只擦除未建文件系统,`/data` 挂载失败 | 用 `fastboot format` / 让系统首启自建 ext4 |
| **机型识别 UNKNOWN** | 纯 fastboot 直刷后机型 UNKNOWN、丢双卡 | fastboot 直刷跳过 recovery 的 `devinfo.sh`,`ro.leeco.devinfo` 停在 `NULL` | device 树对 `NULL`/空值兜底为 `le_x2_whole_netcom`(LEX820) |

---

## 组件仓库索引

本仓库是整个移植工程的**统一入口**。真正的源码分布在以下组件仓,`android_local_manifests` 会在 `repo sync` 时把它们自动拉齐:

| 仓库 | 角色 | 说明 |
| :-- | :-- | :-- |
| [**android_local_manifests**](https://github.com/Pangu-Immortal/android_local_manifests) | 🧭 编排清单 | 一条命令拉齐下方所有树 |
| [**android_device_leeco_x2**](https://github.com/Pangu-Immortal/android_device_leeco_x2) | 📱 设备树 | 分区表、fstab、机型识别、产品定义 |
| [**android_device_leeco_msm8996-common**](https://github.com/Pangu-Immortal/android_device_leeco_msm8996-common) | 🧩 平台 common | 骁龙 820 平台共享 HAL、SEPolicy、通用配置 |
| [**android_kernel_leeco_msm8996**](https://github.com/Pangu-Immortal/android_kernel_leeco_msm8996) | 🐧 内核 | msm8996 定制内核源码 |
| **proprietary_vendor_leeco** 🔒 | 🔐 私有 blobs | 厂商专有二进制 · 私有仓库,版权归原厂所有 |

---

## 从源码构建

> 构建主机建议:Ubuntu 20.04 / 22.04 · 16C/32G 起 · 300 GB+ 可用空间 · 已配置 [LineageOS 构建依赖](https://wiki.lineageos.org/devices/)。

```bash
# 1. 初始化 LineageOS 18.1 源码树
repo init -u https://github.com/LineageOS/android.git -b lineage-18.1 --git-lfs

# 2. 拉入本项目的 local_manifests(自动串起 device / common / kernel / vendor)
git clone https://github.com/Pangu-Immortal/android_local_manifests .repo/local_manifests

# 3. 同步全部源码
repo sync -c --no-clone-bundle --optimized-fetch -j"$(nproc --all)"

# 4. 配置环境并选定机型
source build/envsetup.sh
breakfast lineage_x2-userdebug        # 机型 codename: x2

# 5. 全量构建
brunch x2
# 产物: out/target/product/x2/lineage-18.1-*-x2-signed.zip
```

---

## 刷机指南

> ⚠️ **解锁 Bootloader 会清空全部数据;刷机有变砖风险。刷机前请务必做一份完整分区备份——它是你唯一的后悔药。** 请先确认机型为 Le Max 2(`x2`)。

```bash
# 1. 进入 Bootloader 并解锁(仅首次,会清空数据)
adb reboot bootloader
fastboot oem unlock

# 2. 刷入 LineageOS Recovery 并进入
fastboot flash recovery lineage-18.1-recovery-x2.img
fastboot reboot recovery

# 3. 在 Recovery 中执行 Wipe → Format Data
#    关键一步:解决 msm8996 强制加密导致的 bootloop

# 4. 侧载刷入系统包(首次开机耗时较长,请耐心等待进入桌面)
adb sideload lineage-18.1-*-x2-signed.zip
```

**刷完自检——用证据说话:**

```bash
adb shell getprop ro.build.version.release   # 期望输出: 11
adb shell getprop sys.boot_completed         # 期望输出: 1
adb shell getprop ro.lineage.build.version   # 期望输出: 18.1
```

---

## 路线图

- ✅ **Android 11 / LineageOS 18.1** — 已交付,真机验证通过。
- 🔧 **稳定性打磨** — VoLTE、相机 HAL、睡眠功耗持续优化中。
- 🔬 **Treble / GSI 兼容性探索** — 为运行更新的 AOSP GSI 打通底座。
- 🧭 **更高 Android 版本(含 Android 16 GSI 兼容性验证)** — **进行中的探索方向,尚未交付**;是否可用一切以真机 `build.prop` 为准,绝不提前宣布。

> 我们对「路线图」和「已交付」划清界限:承诺的每一步,都要能在真机上被复现和证伪。

---

<div align="center">

## Star History

<a href="https://star-history.com/#Pangu-Immortal/LeEco-LeMax2-LineageOS&Date"><img src="https://api.star-history.com/svg?repos=Pangu-Immortal/LeEco-LeMax2-LineageOS&type=Date" width="600" alt="Star History"/></a>

<br/><br/>

## 关于作者

**主业 · 大模型算法 / AI 工程 / 端侧 AI** —— 专注大模型落地、Agentic 系统(LangGraph · A2A · MCP · ADK · GraphRAG)、端侧离线多模态推理(手机端 / 车载离线语言与生图生视频、世界模型)。这是我投入最深的战场。

**技术爱好 · 系统底层与逆向** —— ROM 定制、复活老设备与逆向工程是纯工程好奇心的业余钻研,与主业无关,只关热爱。

<br/>

**寻求合作** · 大模型 / Agent 系统落地 · ROM 定制与逆向工程咨询

<a href="mailto:yugu88@126.com"><img src="https://img.shields.io/badge/Email-yugu88@126.com-607D8B?style=flat-square&logo=gmail&logoColor=white" alt="email"/></a>
<a href="https://github.com/Pangu-Immortal"><img src="https://img.shields.io/badge/GitHub-@Pangu--Immortal-78909C?style=flat-square&logo=github&logoColor=white" alt="github"/></a>

<br/><br/>

<sub>本项目以 Apache-2.0 开源,允许商用(内核遵循 GPL-2.0,继承上游)· 与 LeEco / 乐视、Google、Qualcomm、LineageOS 官方无隶属关系 · 设备名及商标归各自所有者所有 · 刷机、解锁 Bootloader 有数据丢失与变砖风险,请自行备份并谨慎操作。</sub>

<img src="https://capsule-render.vercel.app/api?type=waving&color=0:3f2b96,100:a8c0ff&height=100&section=footer" alt="footer"/>

</div>
