<div align="center">

# 🔥 LeEco Le Max 2 · LineageOS 复活计划 `(x2)`

### 官方在 Android 6 抛弃了它 —— 我用源码，让它真机跑上了 Android 11

<br/>

<img src="https://img.shields.io/badge/Device-Le%20Max%202%20%C2%B7%20x2-000000?style=for-the-badge&logo=android&logoColor=white" alt="device">
<img src="https://img.shields.io/badge/SoC-Snapdragon%20820%20%C2%B7%20MSM8996-E4002B?style=for-the-badge&logo=qualcomm&logoColor=white" alt="soc">
<img src="https://img.shields.io/badge/LineageOS-18.1-167C3E?style=for-the-badge&logo=lineageos&logoColor=white" alt="lineageos">
<img src="https://img.shields.io/badge/Android-11-3DDC84?style=for-the-badge&logo=android&logoColor=white" alt="android11">

<br/>

<img src="https://img.shields.io/badge/%E5%AE%98%E6%96%B9%E6%AD%A2%E6%AD%A5-Android%206.0.1-9E9E9E?style=flat-square" alt="stock">
<img src="https://img.shields.io/badge/%E8%A2%AB%E6%8A%9B%E5%BC%83-8%20%E5%B9%B4-757575?style=flat-square" alt="abandoned">
<img src="https://img.shields.io/badge/%E7%89%88%E6%9C%AC%E8%B7%83%E8%BF%81-%2B5%20%E4%B8%AA%E5%A4%A7%E7%89%88%E6%9C%AC-FF6F00?style=flat-square" alt="jump">
<img src="https://img.shields.io/badge/%E7%9C%9F%E6%9C%BA%E9%AA%8C%E8%AF%81-boot__completed%20%E2%9C%93-2E7D32?style=flat-square" alt="verified">
<img src="https://img.shields.io/badge/License-Apache--2.0%20%2F%20GPL--2.0-1565C0?style=flat-square" alt="license">
<img src="https://img.shields.io/github/followers/Pangu-Immortal?label=Follow&style=flat-square&logo=github" alt="follow">

<br/><br/>

**2016 年，骁龙 820 是安卓阵营的性能天花板。乐视把它塞进 Le Max 2，然后止步 Android 6.0.1，停更、解散、抛弃，八年杳无音讯。**
**这个仓库，是它的第二次开机。**

<br/>

`Android 6.0.1` ⛔ ⟶ `7` ⟶ `8` ⟶ `9` ⟶ `10` ⟶ **`Android 11`** ✅ &nbsp;·&nbsp; `Android 16 🧭 路线图探索中`

</div>

---

## 💀 → 🌱 一台旗舰的死与生

> 有些设备不该被时代淘汰，它们只是被停止了维护。

| 时间线 | 状态 | 发生了什么 |
| :--- | :--- | :--- |
| **2016 · 巅峰** | 🏆 旗舰 | 骁龙 820、2K 屏、金属机身——那一年的顶级性能 |
| **2016 年底 · 停摆** | ⛔ 停更 | 官方推送最后一版 **Android 6.0.1** 后，永久沉默 |
| **此后 8 年 · 遗忘** | 🪦 被弃 | 系统冻结在 Android 6，被安全更新、被生态、被时代抛下 |
| **今天 · 重生** | 🌱 复活 | 从 LineageOS **源码级重建**，真机点亮 **Android 11（LineageOS 18.1）** |

我没有等一个永远不会到来的官方更新，而是从 **LineageOS 源码树** 把它一行行重建：设备树、平台 common、内核、vendor blobs 全部自持维护，跨越 **5 个大版本**，把这台八年前的旗舰真机拉到现代 Android。

> 官方抛弃它的地方，就是这个项目开始的地方。

---

## ✅ 真机验证的事实（可被 `build.prop` 复核）

诚实是硬核工程的底线。以下每一项都在真机上跑通、可复现：

| 验证项 | 结果 | 证据来源 |
| :-- | :-: | :-- |
| 系统启动 | ✅ `sys.boot_completed = 1` | `adb shell getprop` |
| 进入桌面 | ✅ Launcher 正常，可交互 | 真机 |
| Android 版本 | ✅ **Android 11**（`ro.build.version.release = 11`） | `build.prop` 可查 |
| 双卡双待 | ✅ 双 SIM 识别正常 | 拨号 / 信号栏 |
| 基带 / 通话 | ✅ 基带在线，可正常拨打接听 | 真机 |
| 移动数据 / WiFi / 蓝牙 | ✅ 联网、配对可用 | 真机 |
| 相机 / 指纹 等 | 🔧 持续完善，以设备仓 Issue 为准 | Issue 跟踪 |
| Android 16 | 🧭 路线图探索中（Treble GSI），**尚未交付** | — |

> 🧭 **不吹牛红线：** 本 ROM 真机稳定运行的版本是 **Android 11 / LineageOS 18.1**。Android 16 仅为持续推进的技术路线，**未交付即不宣称**。我们只写能被真机验证的东西。

---

## 🧨 为什么这台机器难搞

不是「下个源码点一下编译」就能成的活。它难在——

- **官方零支持**：LeEco 已解散，没有维护中的内核、没有新版 blobs、没有官方设备树，一切从零重建。
- **闭源 blobs 断代**：msm8996 平台大量私有二进制停留在旧 vendor，向上适配全靠人肉对齐 HAL 与 SEPolicy。
- **多变体地雷**：Le Max 2 含 `x820 / x821 / x829` 多个子型号，基带、分区、校验各不相同，认错一个就砖。
- **现代工具链断链**：用 2024/2025 的主机去编 2020 的 LOS 18.1，host 侧一路踩雷。

**别人卡在这里放弃，我把每一个坑都填平了。**

---

## 🛠️ 征服的坑 · 工程档案

| 坑 | 症状 | 根因 | 征服方式 |
| :-- | :-- | :-- | :-- |
| **ncurses 断链** | 现代 Ubuntu 上 host 工具链编译中断 | LOS 18.1 部分 host 二进制依赖已被弃用的 `libncurses5` | 补齐 legacy host 依赖、修正 prebuilt 链接，恢复整棵 host 工具链 |
| **LFS 大文件** | `repo sync` 与 `out/` 目录爆炸，git 拒绝写入 | vendor blobs 与 sparse 镜像超出常规文件处理阈值 | 启用 git-lfs + 大文件分区，压平 100 GB+ 构建树 |
| **mke2fs 特性不兼容** | 刷入后 `system` 挂载失败、开机即挂 | 新版 `mke2fs` 默认开 `metadata_csum` / `64bit`，msm8996 引导链读不了 | 锁定 ext4 特性集，回退到设备可挂载的镜像格式 |
| **data 强制加密 bootloop** | 首刷卡在开机动画、循环重启 | msm8996 FBE 与 `fstab` 加密标志不匹配 | 修正 fstab、打通 `Format Data` 流程，跑通首启动解密 |
| **机型识别错乱** | 变体刷错基带 / OTA 校验失败 | 单一设备树未区分 Le Max 2 子型号 | 建立 `x2` codename 映射与 assert 校验，统一多变体识别 |

---

## 🧩 组件仓库索引

本仓库是整个移植工程的**统一入口**。真正的源码分布在以下组件仓，`android_local_manifests` 会在 `repo sync` 时把它们自动拉齐：

| 仓库 | 角色 | 说明 |
| :-- | :-- | :-- |
| [**android_local_manifests**](https://github.com/Pangu-Immortal/android_local_manifests) | 🧭 编排清单 | 一条命令拉齐下方所有树 |
| [**android_device_leeco_x2**](https://github.com/Pangu-Immortal/android_device_leeco_x2) | 📱 设备树 | 分区表、fstab、机型识别、产品定义 |
| [**android_device_leeco_msm8996-common**](https://github.com/Pangu-Immortal/android_device_leeco_msm8996-common) | 🧩 平台 common | 骁龙 820 平台共享 HAL、SEPolicy、通用配置 |
| [**android_kernel_leeco_msm8996**](https://github.com/Pangu-Immortal/android_kernel_leeco_msm8996) | 🐧 内核 | msm8996 定制内核源码 |
| **proprietary_vendor_leeco** 🔒 | 🔐 私有 blobs | 厂商专有二进制 · 私有仓库，版权归原厂所有 |

---

## 🚀 从源码构建

> 构建主机建议：Ubuntu 20.04 / 22.04 · 16C/32G 起 · 300 GB+ 可用空间 · 已配置 [LineageOS 构建依赖](https://wiki.lineageos.org/devices/)。

```bash
# 1. 初始化 LineageOS 18.1 源码树
repo init -u https://github.com/LineageOS/android.git -b lineage-18.1 --git-lfs

# 2. 拉入本项目的 local_manifests（自动串起 device / common / kernel / vendor）
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

## 📲 刷机指南

> ⚠️ **解锁 Bootloader 会清空全部数据；刷机有变砖风险。刷机前请务必做一份完整分区备份——它是你唯一的后悔药。** 请先确认机型为 Le Max 2（`x2`）。

```bash
# 1. 进入 Bootloader 并解锁（仅首次，会清空数据）
adb reboot bootloader
fastboot oem unlock

# 2. 刷入 LineageOS Recovery 并进入
fastboot flash recovery lineage-18.1-recovery-x2.img
fastboot reboot recovery

# 3. 在 Recovery 中执行 Wipe → Format Data
#    关键一步：解决 msm8996 强制加密导致的 bootloop

# 4. 侧载刷入系统包（首次开机耗时较长，请耐心等待进入桌面）
adb sideload lineage-18.1-*-x2-signed.zip
```

**刷完自检——用证据说话：**

```bash
adb shell getprop ro.build.version.release   # 期望输出: 11
adb shell getprop sys.boot_completed         # 期望输出: 1
adb shell getprop ro.lineage.build.version   # 期望输出: 18.1
```

---

## 🗺️ 路线图

- ✅ **Android 11 / LineageOS 18.1** — 已交付，真机验证通过。
- 🔧 **稳定性打磨** — VoLTE、相机 HAL、睡眠功耗持续优化中。
- 🔬 **Treble / GSI 兼容性探索** — 为运行更新的 AOSP GSI 打通底座。
- 🧭 **更高 Android 版本（含 Android 16 GSI 兼容性验证）** — **进行中的探索方向，尚未交付**；是否可用一切以真机 `build.prop` 为准，绝不提前宣布。

> 我们对「路线图」和「已交付」划清界限：承诺的每一步，都要能在真机上被复现和证伪。

---

## 👤 关于作者

**主业 · 大模型算法 / AI 工程** —— 专注 **LLM 应用、Agent 智能体系统、模型工程与落地**：从推理链路、工具编排到生产级 Agent 架构，这是我投入最深、也最认真的战场。

**副业做到顶尖 · Android 定制 ROM 与逆向工程** —— 标准只有一个：做到行业顶流。你正在看的这份「让 2016 年旗舰从 Android 6 复活到 Android 11」的工程，就是这句话的注脚。另一代表作是 **[KeepLiveService](https://github.com/Pangu-Immortal)**——公认高难度的 Android 进程保活方案，系统级与逆向能力的证明。

> 连副业都做到行业顶尖，是我对「工程」两个字的要求。

<div align="center">
<br/>

<img src="https://github-readme-stats.vercel.app/api?username=Pangu-Immortal&show_icons=true&count_private=true&hide_border=true&theme=tokyonight" alt="GitHub Stats" height="165"/>
<img src="https://github-readme-stats.vercel.app/api/top-langs/?username=Pangu-Immortal&layout=compact&hide_border=true&langs_count=8&theme=tokyonight" alt="Top Languages" height="165"/>

</div>

---

<div align="center">

## ⭐ 如果这个「让老设备复活」的故事打动了你

**点一颗 Star，是对这份硬核工程最好的回礼。**
它也会让更多还握着 Le Max 2 的人，知道这台老旗舰还能再战。

<br/>

**寻求合作** · 大模型 / Agent 系统落地 · ROM 定制与逆向工程咨询

<br/>

<a href="mailto:yugu88@126.com"><img src="https://img.shields.io/badge/Email-yugu88@126.com-D14836?style=for-the-badge&logo=gmail&logoColor=white" alt="email"/></a>
<a href="https://github.com/Pangu-Immortal"><img src="https://img.shields.io/badge/GitHub-@Pangu--Immortal-181717?style=for-the-badge&logo=github&logoColor=white" alt="github"/></a>

<br/><br/>

<sub>本项目以 Apache-2.0 开源（内核遵循 GPL-2.0，继承上游）· 与 LeEco / 乐视、Google、Qualcomm、LineageOS 官方无隶属关系 · 设备名及商标归各自所有者所有 · 刷机、解锁 Bootloader 有数据丢失与变砖风险，请自行备份并谨慎操作。</sub>

</div>
