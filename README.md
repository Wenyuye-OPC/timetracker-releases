# 时行 · 发版

这个仓库只放安装包和一份发版清单，不含源码。

- `latest.json` — App 每天读一次的发版清单
- Releases — 各版本的 APK

## 发新版本的步骤

1. 在源码仓库把 `versionCode` 升一号、`versionName` 改成新版本号
2. `./gradlew assembleRelease`（必须用同一把 `release.keystore` 签，
   换了签名老用户就永远装不上了）
3. 在本仓库建一个 tag 为 `v<版本名>` 的 Release，把 APK 传上去
4. 改 `latest.json`：`versionCode` / `versionName` / `apkUrl` / `sizeBytes` / `notes`
   都要跟着改，`sizeBytes` 填 APK 的真实字节数
5. 提交到 `main`

第 4 步漏改任何一项，用户那边要么收不到提示，要么下到一个装不上的包。

## latest.json 的字段

| 字段 | 必填 | 说明 |
|---|---|---|
| `versionCode` | 是 | 正整数，唯一的新旧判据。版本名不参与比较 |
| `versionName` | 是 | 给人看的版本号，最长 32 字 |
| `apkUrl` | 是 | **必须是 https**，http 会被 App 直接拒绝 |
| `sizeBytes` | 否 | APK 字节数，用来校验下载是否完整 |
| `notes` | 否 | 更新说明，直接显示在对话框里 |
