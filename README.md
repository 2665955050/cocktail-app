# 鸡尾酒助手 · Android APK（云端编译）

这个仓库不包含 Android 工程——`android/` 目录由 GitHub Actions 在云端用 Capacitor 现场生成，编译出 `app-debug.apk`。你本地什么都不用装。

## 一次性步骤

1. **建仓库**：GitHub 右上角 `+` → New repository → 名字随便（比如 `cocktail-app`）→ 选 **Public** → **不要**勾 "Add a README file" → Create。
2. **传文件**：在新仓库页面点 `uploading an existing file`，把本文件夹里的这些东西拖进去：
   - `package.json`
   - `capacitor.config.json`
   - `.gitignore`
   - `www/`（整个文件夹，里面是 `index.html`）
   - `.github/`（整个文件夹，里面有 `workflows/build-apk.yml`）

   > 如果 `.github` 这个以点开头的文件夹拖不进去（浏览器有时会跳过隐藏文件夹），就手动建：`Add file` → `Create new file` → 文件名填 `.github/workflows/build-apk.yml` → 把本地这个文件的内容粘进去 → Commit。

3. **等编译**：点仓库顶部的 `Actions`，会看到一个叫 `build-apk` 的任务在跑。首次大约 3–6 分钟。
4. **拿 APK**：点进那次运行 → 页面底部 `Artifacts` → 下载 `cocktail-apk.zip` → 解压得到 `app-debug.apk`。
5. **发给朋友**：微信/QQ 传文件都行。对方安装时要允许"安装未知应用"。

## 以后改内容

只改 `www/index.html`（这是整个应用，单文件），提交后 Actions 自动重跑，几分钟后就有新 APK。

## 说明

- 这是 **debug 包**，用调试证书签名，能装能跑，但不能上架应用商店。
- 网页资源打在包里，**离线可用**，不依赖任何网址。
- 应用数据（酒柜勾选、练习记录）存在手机本地，卸载会清空。
- 包名 `com.cocktail.assistant`，想改就改 `capacitor.config.json` 的 `appId`（改完要重新生成，Actions 每次都会重新生成，所以直接改就行）。
