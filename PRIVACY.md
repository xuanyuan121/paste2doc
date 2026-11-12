# 隐私政策 · 内容直贴 Paste2Doc

最后更新：2026-11-12　适用版本：0.1.8 及以后

---

## 一句话

**这个扩展不收集、不上传、不存储你的任何内容。运行时不联网。
唯一的一次网络请求，是你主动点「下载本地组件」时去取那个安装包。**

---

## 一、它读什么

- **只在你在页面上点击之后**，读取你点到的那一条回答（或那一段、那个区间）的文字与结构，
  用来生成一份排好版的文档放进剪贴板。
- 为了判断"哪里是正文"，它会在页面上查找正文容器、标题、列表、表格、公式这些结构，
  以及"这是不是思考过程 / 这是不是你自己的提问"。**这些判断全部在当前页面内完成，
  结果不会离开浏览器。**
- 它**不收集**浏览历史、不收集你访问过哪些网站、不读取页面上你没选中的内容、
  不读取输入框里你正在打的字。

## 二、它写什么

- **剪贴板**：只写不读。写入的内容就是你刚刚选中的那段回答（已排版的文档格式，
  或纯文本）。扩展从不读取剪贴板里已有的内容。
- **本地偏好**：复制方式（全文 / 单段 / 区间）、排版选项（统一排版或保留原格式、
  首行缩进、字号、行距）、是否只复制纯文本。这些存在浏览器自带的
  `chrome.storage.sync` 里，仅用于记住你的选择。**它们会随浏览器账号同步到你自己
  的其他设备，这是浏览器提供的能力；不会发到我们或任何第三方的服务器。**

## 三、本地组件（可选）

WPS 文字只接受它自己专用的剪贴板格式（`Kingsoft WPS 9.0 Format`），浏览器没有写入
这种格式的接口，因此需要一个很小的本地组件代写一下。它：

- 由浏览器按需拉起，处理完当前这次复制后空闲退出，**不开机自启、不常驻**；
- **不联网**（代码中没有任何网络请求，也没有 URL 配置）；
- **不读写你的文件**，不执行系统命令；
- 只做一件事：把扩展已经算好的内容按 WPS / Word 的格式写进剪贴板；
- 安装程序（`安装本地组件.bat`）在**你选择**「下载一个 Python」之后，才会去你选的那个
  镜像（华为云 / npmmirror / python.org）取官方 Python 安装包，装到当前用户下；
  不选就不会下载任何东西；
- 卸载方式：双击 `卸载本地组件.bat`（它删掉注册表
  `HKCU\Software\Google\Chrome\NativeMessagingHosts\com.paste2doc.host`、
  `HKCU\Software\Microsoft\Edge\NativeMessagingHosts\com.paste2doc.host` 和
  `...\Chromium\...` 三条登记，以及安装时生成的启动脚本），不会留下后台进程。

不装本地组件时扩展依然可用，只是复制出来的是纯文本。

## 四、网络

**扩展在运行时不发起任何网络请求。** 没有账号、没有登录、没有统计、没有埋点、
没有远程配置、没有远程代码。公式渲染用的 KaTeX 是打包在扩展里的本地文件，
不从 CDN 加载。

唯一的例外在侧边栏：当浏览器里没有本地组件时，侧边栏会显示一块「本地组件未安装」，
上面有一个「下载本地组件」按钮。**只有你点它**，扩展才会去我们的下载页取那个
安装包（`download-host.zip`，36 KB 左右）。这次请求只带标准 HTTP 头，
**不包含你的任何内容、不包含任何标识符**；服务器能看到的就是你的 IP 和这次下载本身，
我们没有为此设置任何日志或统计。取回来之后由浏览器保存到你本机的下载目录，
扩展不会再访问网络，直到你下次点那个按钮。

## 五、第三方

扩展内打包了开源组件 KaTeX（MIT 许可），版权归 Khan Academy 及贡献者所有，
清单见 `THIRD-PARTY-NOTICES.txt`。除此之外没有其他第三方代码、SDK 或服务。

## 六、儿童

本扩展不面向 13 岁以下儿童，也不收集任何人的个人信息。

## 七、变更

本政策如有变更，会更新本文件的日期，并在扩展更新说明里写清改了什么。

## 八、联系

问题、疑问或数据相关请求：通过扩展商店详情页的「支持」入口，或在
<https://github.com/xuanyuan121/paste2doc/issues> 提 issue。

---

# Privacy Policy · Paste2Doc

Last updated: 2026-11-12　Applies to: 0.1.8 and later

**Short version: this extension does not collect, store, or transmit any of your
content. It makes no network requests at runtime. The single exception is the
"Download local component" button, which fetches that installer when you click it.**

## What it reads

Only after you click, it reads the answer (or the single block, or the range) you
pointed at, in order to build a formatted document on your clipboard. To decide
what counts as body text it inspects page structure — content containers,
headings, lists, tables, formulas, and whether something is a "thinking" panel or
your own question. All of that happens inside the page; nothing leaves the
browser. It does not collect browsing history, does not read content you did not
select, and does not read what you type.

## What it writes

- **Clipboard**: write-only. It writes the answer you just selected. It never
  reads the existing clipboard.
- **Preferences**: copy mode, formatting options, plain-text toggle. Stored in
  `chrome.storage.sync` so the browser can remember them for you. They are never
  sent to us or to any third party.

## Optional local component

WPS Writer only accepts its proprietary clipboard format, which browsers cannot
write, so a small optional local helper writes it for you. It is launched on
demand by the browser, exits when idle, does not start at login, makes no network
requests, does not read or write your files, and does not execute commands.
Without it the extension still works, producing plain text. Its installer only
downloads a Python runtime if you explicitly pick one of the offered mirrors.

## Network

No network requests from the extension at runtime. No account, no analytics,
no telemetry, no remote configuration, no remote code. KaTeX is bundled locally.

The single exception: when no local component is installed, the side panel shows
a "Download local component" button. Only if you click it does the extension
fetch that installer (about 36 KB) from our download page. The request carries
standard HTTP headers only — none of your content and no identifier; the server
sees your IP and the download itself, and we keep no logs or analytics for it.
After saving the file the extension makes no further requests until you click
that button again.

## Contact

Use the support link on the store listing, or open an issue at
<https://github.com/xuanyuan121/paste2doc/issues>.
