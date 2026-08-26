<div align="center">

# 🌙 DMode Evolution

**为 MIUI 14 / 13 补全第三方应用深色模式的 Magisk 模块**

[![Release](https://img.shields.io/github/v/release/f1owkang/DModeEvolution?style=flat-square&label=Release&color=blue)](https://github.com/f1owkang/DModeEvolution/releases)
[![Downloads](https://img.shields.io/github/downloads/f1owkang/DModeEvolution/total?style=flat-square&label=Downloads&color=green)](https://github.com/f1owkang/DModeEvolution/releases)
![Language](https://img.shields.io/badge/Language-Shell-89e051?style=flat-square&logo=gnu-bash&logoColor=white)
![Platform](https://img.shields.io/badge/Platform-MIUI_13_%7C_14-ff6900?style=flat-square&logo=xiaomi&logoColor=white)
[![License](https://img.shields.io/badge/License-MIT-orange?style=flat-square)](LICENSE)

[支持应用](#支持应用) · [安装使用](#安装使用) · [进阶教程](#进阶教程) · [已知问题](#已知问题) · [致谢名单](#致谢名单)

</div>

> [!WARNING]
> **本项目已停止维护，仓库仅作存档保留。**<br>
> 模块兼容 MIUI 14 / 13，但存在 **自动重启进入 Recovery**、**卡在第一屏** 等已知风险，刷入前请务必备份数据并自行评估。

---

## 模块简介

MIUI 的强制深色模式默认仅覆盖少量系统应用，大量第三方应用无缘深色。本模块通过补全 MIUI 的深色模式配置——总开关 `ForceDarkAppSettings.json` 与单应用增强配置 `forcedarkconfig/`——让更多应用接入系统级深色模式。刷入后，可在 **设置 → 显示 → 更多深色模式设置** 中按应用单独控制开关。

安装脚本会在刷入时自动检测设备环境：

- 通过音量键交互确认安装（音量+ 确认 / 音量- 取消）
- 自动区分 MIUI 13（`system/etc`）与 MIUI 14（`system_ext/etc`）的配置路径，无需手动选择版本

## 支持应用

● 兼容良好　◐ 效果一般　○ 未经确认

| 状态 | 应用 | 包名 |
| :--: | :-- | :-- |
| ● | 淘宝 | `com.taobao.taobao` |
| ● | 学习通 | `com.chaoxing.mobile` |
| ◐ | 闲鱼 | `com.taobao.idlefish` |
| ● | 阿里巴巴 | `com.alibaba.wireless` |
| ◐ | 铁路12306 | `com.MobileTicket` |
| ◐ | 支付宝 | `com.eg.android.AlipayGphone` |
| ● | 什么值得买 | `com.smzdm.client.android` |
| ◐ | 抖音 | `com.ss.android.ugc.aweme` |
| ● | 拼多多 | `com.xunmeng.pinduoduo` |
| ○ | 高德地图 | `com.autonavi.minimap` |

> 以上仅为部分示例，完整支持列表见模块内置的 [`ForceDarkAppSettings.json`](system/etc/ForceDarkAppSettings.json) 与 [`forcedarkconfig/`](system/etc/forcedarkconfig) 目录。

## 安装使用

1. 前往 [**Releases**](https://github.com/f1owkang/DModeEvolution/releases) 下载最新 zip 包
2. 打开 **Magisk** →「模块」→「从本地安装」，选择刚下载的 zip
3. 安装过程中按提示用音量键确认（音量+ 安装 / 音量- 取消）
4. 安装完成后重启手机
5. 进入 **设置 → 显示 → 更多深色模式设置**，为需要的应用打开开关

## 已知问题

- 部分应用的配置自 MIUI 14 起已失效；因项目停止维护，不再跟进修复
- 抖音（`com.ss.android.ugc.aweme`）内测版已自带深色模式，无需本模块

## 简明教程

<details>
<summary><b>Q：如何让模块支持我想深色化的应用？</b></summary>

MIUI 通过两类配置文件控制应用的深色模式：

- **`ForceDarkAppSettings.json`**：总开关，必须修改
- **`forcedarkconfig/`**：单应用增强配置，仅在总开关效果不佳或不生效时使用

操作步骤：

1. 查询目标应用的包名，例如 `com.dark.demo`
2. 在 `ForceDarkAppSettings.json` 的 `[]` 数组中追加一行：

```json
{"defaultEnable":false,"overrideEnableValue":0,"packageName":"com.dark.demo","showInSettings":true}
```

| 参数 | 含义 |
| :-- | :-- |
| `defaultEnable` | 是否默认开启深色，可选 `true` / `false` |
| `showInSettings` | 是否在系统设置中显示该应用的开关 |

3. 修改后用 [JSON 格式校验器](https://json-online.com/check/) 验证文件合法性，重新刷入模块即可

正常情况下到这里就能生效；若无效，请继续查看进阶教程。

</details>

## 进阶教程

<details>
<summary><b>Q：如何为应用编写增强配置文件？</b></summary>

当总开关配置效果不理想时，可以为单个应用编写增强配置：

1. 查询目标应用包名，例如 `com.dark.demo`
2. 在 `forcedarkconfig/` 目录下新建 `com.dark.demo.json`，写入以下模板：

```json
{
  "packageName": "com.dark.demo",
  "forceDark": true,
  "mainRule": 0,
  "forceDarkActivityConfigList": [],
  "forceDarkViewGlobalConfigList": []
}
```

3. 根据实际效果调整各参数并多次测试（原《小米深色配置.xlsx》参数说明已过时，随仓库移除）

</details>

## 致谢名单

- 酷安 @夜夜夜猫
- GitHub [@MidNightBlackCat](https://github.com/MidNightBlackCat)
- GitHub [@dreamflandre](https://github.com/dreamflandre) —— MIUI 14 适配思路参考自 [DarkP](https://github.com/dreamflandre/DarkP/releases)
- 安装脚本：酷安 @阿巴酱
- 以及所有在酷安支持过这个项目的朋友们

喜欢本项目的话，欢迎提交 PR 或点亮 Star。完整更新记录见 [changelog.md](changelog.md)。

## 开源协议

本项目基于 [MIT License](LICENSE) 开源。

---

<div align="center">

**Made with ❤ by [f1owkang](https://github.com/f1owkang)**

</div>
