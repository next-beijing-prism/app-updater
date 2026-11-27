# app-updater

「星轨计划·北京」App 的在线更新仓库。App 内「检查更新」读取本仓库的 `latest.json` 版本清单，发现新版本后从本仓库 `apk/` 目录下载安装包。

## 文件结构

```
latest.json                      版本清单（App 更新检查入口）
apk/                             安装包（APK 直接分发）
```

## 地址

- 清单（raw）：`https://raw.githubusercontent.com/next-beijing-prism/app-updater/main/latest.json`
- 清单（jsDelivr 镜像，App 的备用地址）：`https://cdn.jsdelivr.net/gh/next-beijing-prism/app-updater@main/latest.json`
- 仓库主页：https://github.com/next-beijing-prism/app-updater

## 发布新版本流程

1. 将新 APK 放入 `apk/`（文件名含版本号）
2. 修改 `latest.json`：更新 `version`、`versionCode`、`notes` 与 `downloadUrl` 指向新 APK
3. 提交推送即可，App 端下次检查更新即会提示（版本号按语义化比较，versionCode 仅作展示）

## 清单格式

```json
{
  "version": "1.2.0.2",
  "versionCode": 1202,
  "updatedAt": "2026-11-27",
  "mobile": {
    "version": "1.2.0.2",
    "versionCode": 1202,
    "notes": [{ "text": "更新说明，每条一行" }],
    "downloadUrl": "https://raw.githubusercontent.com/next-beijing-prism/app-updater/main/apk/<文件名>.apk"
  }
}
```

## 相关仓库

- 资讯数据源：https://gitee.com/next-studio/news
