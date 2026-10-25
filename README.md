# 波兰语练习（Android App）

把 `www/index.html` 这个网页应用，用 [Capacitor](https://capacitorjs.com) 打包成原生安卓 App。
代码推送到 GitHub 后，GitHub Actions 会自动编译并签名出 APK。

## 一、上传到 GitHub（手机/电脑都行）

1. 在 GitHub 新建一个仓库（建议选 **Private** 私有，因为签名密钥在仓库里）。
2. 把本文件夹里的**所有文件**上传到仓库根目录（包括隐藏文件夹 `.github`）。
   - 电脑上最省事：安装 Git，在本文件夹执行
     ```bash
     git init && git add -A && git commit -m "init"
     git branch -M main
     git remote add origin https://github.com/你的用户名/仓库名.git
     git push -u origin main
     ```
3. 推送后打开仓库的 **Actions** 页，会看到 “Build Android APK” 在运行，约 5–8 分钟。

## 二、下载 APK

- 仓库右侧 **Releases** 里会出现 `波兰语练习 1.0.N`，手机浏览器直接下载 `.apk` 安装即可。
- 也可以在 Actions 运行记录的 **Artifacts** 里下载（需要登录 GitHub）。
- 安装时手机会提示“允许安装未知来源应用”，允许即可。

之后每次推送到 `main`，都会自动生成新版本（版本号随构建次数递增，可直接覆盖安装，学习数据保留）。

## 三、修改应用

只需要改 `www/index.html`，推送即可自动重新打包。

本地调试（可选）：
```bash
npm install
npx cap sync android
npx cap open android   # 用 Android Studio 打开
```

## 四、签名说明

`android/keystore/polish-release.jks` 和 `android/keystore.properties` 是自动生成的个人签名密钥。
同一个密钥签名的包才能互相覆盖升级，**请不要删除**。
如果仓库要公开，请先换成你自己的密钥并改用 GitHub Secrets。

## 五、联网说明

本应用没有任何内置句子，全部走网络，**没有网络就无法使用**：

- 句子：Tatoeba 随机波兰语句子（含中文翻译）
- 查词：Google 翻译
- 发音：Google 翻译的波兰语语音

## 六、从旧版网页迁移学习记录

在旧网页的浏览器里打开开发者控制台执行 `copy(localStorage.mojPolski_v1)`，
然后在新 App 的 设置 → 备份与恢复 里粘贴并导入。
