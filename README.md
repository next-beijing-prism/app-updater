# app-updater

「星轨计划·北京」App 的在线更新仓库，采用**双通道**发布：正式版（stable）与内测版（beta）。App 内「检查更新」按用户选择的渠道读取对应 `latest.json`，发现新版本后从本仓库下载安装包。

## 文件结构

```
latest.json                        根清单（正式版副本，兼容旧版客户端）
stable/
  latest.json                      正式版清单
  StarTrack-Beijing_1.2.0_1200.apk 正式版安装包（versionCode 1200）
beta/
  latest.json                      内测版清单
  StarTrack-Beijing_1.2.0.2-R-beta_1202.apk  内测版安装包（versionCode 1202）
```

## 命名规范

| 渠道 | 版本号 | versionCode | 示例 |
|---|---|---|---|
| 正式版 stable | 三段式 `1.2.0`、`1.2.1` | `1200`、`1210` | minor 位 ×10 |
| 内测版 beta | 四段式 `1.2.0.1`、`1.2.0.2` | `1201`、`1202` | 在正式版 code 基础上递增 |

## 更新规则

- 渠道在 App「设置 → 参与内测」中选择，默认正式版
- **正式版用户**：只检查 `stable/latest.json`，且新版本号必须大于当前版本号（如 1210 > 1201）才允许更新
- **内测用户**：同时检查 `beta/latest.json` 与 `stable/latest.json`，多个可更新项时取 versionCode 更高的一个；同样要求版本号大于当前版本号
- 版本比较：version 字符串语义化比较 + versionCode 数值比较，两者都须更大

## 地址

- 正式版清单：`https://raw.githubusercontent.com/next-beijing-prism/app-updater/main/stable/latest.json`
- 内测版清单：`https://raw.githubusercontent.com/next-beijing-prism/app-updater/main/beta/latest.json`
- jsDelivr 镜像：`https://cdn.jsdelivr.net/gh/next-beijing-prism/app-updater@main/<stable|beta>/latest.json`
- 仓库主页：https://github.com/next-beijing-prism/app-updater

## 发布流程

1. 将新 APK 放入对应渠道目录（文件名含版本号与 versionCode）
2. 修改该渠道的 `latest.json`：更新 `version`、`versionCode`、`notes`、`downloadUrl`
3. 若发布了新正式版，同步更新根 `latest.json`
4. 提交推送即可，App 端下次检查更新即会提示

## 清单格式（stable/latest.json 与 beta/latest.json 相同）

```json
{
  "version": "1.2.0",
  "versionCode": 1200,
  "updatedAt": "2026-11-27",
  "mobile": {
    "version": "1.2.0",
    "versionCode": 1200,
    "notes": [{ "text": "更新说明，每条一行" }],
    "downloadUrl": "https://raw.githubusercontent.com/next-beijing-prism/app-updater/main/stable/<文件名>.apk"
  }
}
```

## 相关仓库

- 资讯数据源：https://gitee.com/next-studio/news
