# 2024 年 12 月


## 12 月完成的工作
### 更新图形驱动程序的新文档

希望将 Linux 中的新 DRM 驱动程序支持添加到 FreeBSD 的开发者，现在可以按照一套 [说明](https://github.com/freebsd/drm-kmod/wiki/Porting-a-new-version-of-DRM-drivers-from-Linux) 提交 PR 到 [drm-kmod](https://github.com/freebsd/drm-kmod)。

这项工作很有帮助，因为它将社区的知识记录下来，并以一种格式进行共享，使更多的人能够帮助更新图形驱动程序。

>**注意**
>
>我们的项目目标是通过更新到更新的 Linux 版本来逐步推进，最终目标是达到 Linux 6.12。

GitHub 问题： [https://github.com/FreeBSDFoundation/proj-laptop/issues/12](https://github.com/FreeBSDFoundation/proj-laptop/issues/12)

### 针对英特尔 WiFi 接口的驱动程序（基于 OpenBSD/Haiku）

为了创建 FreeBSD 的首个实现版本（概念验证）的 iwx 驱动程序，源代码从 OpenBSD 以 Haiku 导入，进行了最小修改以创建一个可用的驱动程序。我们进行此项工作是为了理解将 WiFi 驱动程序引入 FreeBSD 的不同方法所涉及的工作量和维护工作——基于 LinuxKPI 的 iwlwifi 驱动程序仍然得到支持。

该驱动程序目前已实现网络关联，并且在 802.11a/b/g 网络中具有完整功能，能够在 `a` 和 `g` 频段达到理论上的最大传输速率。

此驱动程序故意设计了不稳定性，以加速崩溃检测，并在虚拟机环境中表现出合理的稳定性。

在 Future Crew 12 月发布 iwx 源代码后，已集成更多功能和 FreeBSD 特定的功能。概念验证阶段现已完成，1月的开发将专注于启用 HT 速率，并为更广泛的用户测试准备驱动程序。

>**注意**
>
>该驱动程序目前仍在积极开发中，尚不建议用于生产环境。

GitHub 问题：[https://github.com/FreeBSDFoundation/proj-laptop/issues/45](https://github.com/FreeBSDFoundation/proj-laptop/issues/45)

## 12月提交审查的工作

### Linux 6.7 的图形驱动程序

已将 DRM 驱动程序代码从 Linux 6.7 移植到 `drm-kmod`。对 i915 和 amdgpu 驱动程序进行的测试，涵盖了编码、浏览和视频播放等常见任务，未发现回归问题。

i915 驱动程序中仍然存在一个长期存在的 bug，表现为终端显示的损坏。该问题是由于在初始化集成 i915 驱动程序与 vt(4) 的代码时未能注册虚拟内存范围造成的。

作为 1 月工作的部分，这个 bug 将得到解决，随后上游的更改将提交给 linuxkpi，FreeBSD 的更改将考虑合并。

GitHub 问题：[https://github.com/FreeBSDFoundation/proj-laptop/issues/47](https://github.com/FreeBSDFoundation/proj-laptop/issues/47)

## 更新进展

### 兼容性和系统要求
#### 笔记本型号

我们正在建立 [笔记本列表](../supported/laptops.md)，用于我们开发和测试的工作。目前，我们已承诺支持一款型号：[Framework Laptop 13 - AMD Ryzen 7040™ Series](https://frame.work/ca/en/products/laptop-diy-13-gen-amd/configuration/new)。如果你希望参与讨论哪些笔记本将被列入支持清单，我们鼓励你 [加入桌面邮件列表](https://lists.freebsd.org/subscription/freebsd-desktop)。

#### 桌面环境兼容性

我们正在建立一个 [桌面环境列表](../supported/desktop-environment.md)，用于我们开发和测试的工作。目前，我们已承诺支持桌面环境：KDE 配合 Wayland。
如果你希望参与讨论哪些桌面环境将被列入支持清单，我们鼓励你 [加入桌面邮件列表](https://lists.freebsd.org/subscription/freebsd-desktop)。

### 安装和系统管理

12月的工作已经开始解决 [pkg 中的技术负担](https://github.com/FreeBSDFoundation/proj-laptop/issues/46)，以支持将来在安装程序中安装 pkgbase 的开发。[我们还将创建一个工具，让用户过渡到使用 pkgbase](https://github.com/FreeBSDFoundation/proj-laptop/issues/26)。

### 错误修复和技术负担管理

除了处理 pkg 中的技术负担（见上文），还修复了设备电源状态切换的问题 ([D48385](https://reviews.freebsd.org/D48385))，以遵循设备在进入低功耗空闲状态时所需的约束（这是 [实现 S0ix 低功耗状态和 s2idle](https://github.com/FreeBSDFoundation/proj-laptop/issues/32) 的一部分）。

支持实现更新 WiFi 标准的工作包括持续开发 [Linux 驱动程序在 FreeBSD 上的翻译层](https://github.com/FreeBSDFoundation/proj-laptop/issues/30)。

## 总结

基金会要对所有帮助启动项目并在本月取得如此有意义进展的人员表示衷心的感谢。

特别感谢：
* 我们的开发者
  * Aymeric Wibo
  * Bjoern Zeeb
  * Christos Margiolis
  * Isaac Freund
  * Jean-Sebastien Pedron
  * Li-Wen Hsu
  * Mitchell Horne
  * Olivier Certner
  * Thinker Li
  * Tom Jones
* 项目团队：
  * Deb Goodkin
  * Ed Maste
  * Joe Mingrone
  * Alice Sowerby
* 笔记本和桌面工作组
  * Chris Moerz
  * 所有与会者
* FreeBSD 项目
* Quantum Leap Research

有关更多信息，请参阅 [README](../README.md) 中的内容，了解 FreeBSD 基金会的笔记本项目。
