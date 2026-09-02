# BJFU WiFi 校园网快速重连

面向 iPhone/iPad Safari 的纯静态 PWA，无构建工具、无后端、无账号密码上传。

## 部署

### GitHub Pages
将本目录推送到仓库，在 **Settings → Pages** 选择 `Deploy from a branch`，选择默认分支的根目录并保存。等待生成 `https://用户名.github.io/仓库名/`。

### Cloudflare Pages
新建 Pages 项目并连接 Git 仓库；Framework preset 选 **None**，Build command 留空，Output directory 填 `/`（或项目目录）。也可直接上传本目录。

### 任意静态服务器
把全部文件保持目录结构上传到网站根目录，用 HTTPS 提供 `index.html`。Service Worker 必须通过 HTTPS（localhost 除外）。

## iPhone / iPad 添加到主屏幕

首次能上网时用 Safari 打开部署网址，点分享按钮 → **添加到主屏幕** → 添加。之后即使已连接 BJFU WiFi 但尚未通过公网认证，也可从主屏幕打开缓存页面。

## 使用与安全

首次输入学号和密码，默认只保存账号。只有明确确认警告后才会保存密码，而且仅存于当前浏览器的 localStorage，不是系统钥匙串；共享设备请勿开启。页面没有统计、分析、后端或网络请求用于收集凭据。

“自动重连”只在页面启动时触发一次提交，不会循环刷新。认证过程使用原生 HTML GET 表单导航到 `http://10.1.1.10/drcom/login`，刻意不使用 `fetch`：HTTPS 托管页面访问 HTTP 校园网地址时，fetch 会受到混合内容/CORS 限制，而浏览器导航/表单提交可避免该问题。认证依赖设备已连接校园 WiFi。

## 可选的自定义

认证参数集中写在 `index.html` 的隐藏表单字段中。若学校接口变化，按实际接口更新字段后重新部署。图标使用内置 SVG 占位图标，无需额外图片构建步骤。
