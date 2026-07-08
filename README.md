<div align="center">

# 📱 LineageOS 18.1 (Android 11) · LeEco Le Max 2

**从源码自建、可长期维护的乐视 Le Max 2（x2 / LEX820 / 骁龙820）Android 11 移植**

`codename x2` · `MSM8996` · `LEX820 全网通` · 官方 LineageOS 支持的最高版本

[![Build](https://img.shields.io/badge/LineageOS-18.1-brightgreen)]() [![Android](https://img.shields.io/badge/Android-11-3ddc84)]() [![SoC](https://img.shields.io/badge/SoC-MSM8996%20(骁龙820)-orange)]() [![状态](https://img.shields.io/badge/状态-真机验证通过-success)]()

</div>

---

## 这是什么

把一台跑 Android 9 的乐视 Le Max 2，**从源码构建并刷成 LineageOS 18.1 (Android 11)**，真机验证 `boot_completed=1`、进桌面、双卡/基带/机型全部正常。这是该设备官方与社区设备树能达到的**最高版本**。

> 本仓库是**统一入口**（build 文档 + 刷机指南 + 组件索引）。想直接编译看 [构建步骤](#构建步骤)。

## 组件仓库（`repo` 多仓库，非 fork，保留上游 LICENSE）

| 仓库 | 作用 |
|---|---|
| [android_device_leeco_x2](../../../android_device_leeco_x2) | x2 设备树（含 `PRODUCT_ADB_KEYS` 等本地修复） |
| [android_device_leeco_msm8996-common](../../../android_device_leeco_msm8996-common) | MSM8996 公共树（含 `ro.leeco.devinfo` 兜底修复） |
| [android_kernel_leeco_msm8996](../../../android_kernel_leeco_msm8996) | 内核源码（msm-3.18 CAF） |
| `proprietary_vendor_leeco` 🔒 | 专有 blobs（私有，源自 TheMuppets） |
| [android_local_manifests](../../../android_local_manifests) | 组装清单 `x2.xml` |

## 构建步骤

```bash
mkdir lineage-18.1 && cd lineage-18.1
repo init -u https://github.com/LineageOS/android.git -b lineage-18.1 --depth=1
mkdir -p .repo/local_manifests
curl -o .repo/local_manifests/x2.xml \
  https://raw.githubusercontent.com/Pangu-Immortal/android_local_manifests/lineage-18.1/x2.xml
repo sync -c -j8 --no-tags --no-clone-bundle
source build/envsetup.sh && breakfast x2 && brunch x2
```

## 刷机（bootloader 需解锁）

```bash
adb reboot bootloader
fastboot flash boot boot.img && fastboot flash system system.img
fastboot flash vendor vendor.img && fastboot flash recovery recovery.img
fastboot format userdata && fastboot format cache   # ⚠️ 必须 format 不是 erase
fastboot reboot
```

## 新宿主机（如 Ubuntu 26.04）编译踩坑速查

| 现象 | 修复 |
|---|---|
| clang 缺 `libncurses.so.5`/`libtinfo.so.5` | 建 `.so.6→.so.5` 系统符号链接 + `ldconfig` |
| `webview.apk` 是 Git LFS 指针 | 单独 clone `..._prebuilt_arm64` + `git lfs pull` 拷真身 |
| `mke2fs: Invalid ...orphan_file` | `sudo sed -i 's/,orphan_file//g' /etc/mke2fs.conf` |
| 卡开机动画（credstore 崩） | 换 ROM 用 `fastboot format userdata`，**别用 erase** |
| 机型显示 `UNKNOWN` | fastboot 直刷跳过 `devinfo.sh`；common 树已加 `ro.leeco.devinfo` 兜底 |

完整说明见各组件仓库与 [android_local_manifests](../../../android_local_manifests)。

---

<div align="center">
上游基于 LineageOS / TheMuppets，遵循各自开源许可（Apache-2.0 等）。
</div>
