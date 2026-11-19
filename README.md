# 小白主页 · 开源个人主页模板

> UI 来自 **孟白** · https://mbclaw.top 　｜　使用和二次发布都必须在页面最下方保留署名链接，见文末「许可」。

一个文件就是一个个人主页：深色毛玻璃、跟着音乐飘的粒子、会被风吹散的歌词、站内看大图、每分钟刷新的实时状态卡。不用框架，不用打包，改改文字就能上线。

**在线预览**：https://mengbaiyoudianxian.github.io/xiaobai-homepage/
**作者本人的主页**（就是用它做的）：https://mbclaw.top/matery-cn/about/

## 有什么

- **顶部栏音乐播放器**：头像做成黑胶唱片，播放时慢慢转；单独的播放 / 暂停键；能自动播放就自动播放，被浏览器拦了就等访客第一次点击、按键、触摸时再放；访客手动暂停过，下次就不自动放。
- **随风粒子**：顶部栏里的光点从下往上飘，用 Web Audio 实时分析音乐，鼓点时从底部推上来一道看不见的声浪，粒子被托一把、亮一下。
- **歌词**：读 LRC 格式歌词，当前句在左、下一句在右；换句时旧歌词从左往右被风吹成细粉，飘散到整条栏里。
- **项目卡片**：两列网格，可以有一张通栏大卡；每张卡有标签、简介、「展开」详情、按钮；鼠标移上去有光斑和轻微倾斜。
- **截图墙 + 看图层**：点截图在页面里放大，← → 键、按钮、手机左右滑切换，Esc / 点空白 / 下滑关闭；先用缩略图顶上，大图下完再换清晰。
- **实时状态卡**：读两个 JSON 文件显示在线、心情、此刻在做什么和四个数字，每分钟刷新，超过 10 分钟没更新自动显示离线。
- **其他**：背景光晕跟随鼠标、滚动进场动画、顶部阅读进度条、手机自适应、尊重「减少动态效果」系统设置。

## 怎么用

1. 下载或 fork 这个仓库。
2. 打开 `index.html`，把这些地方换成你自己的：
   - `<title>`、`<meta name="description">`
   - 顶部栏和首屏里的「你的名字 / YourName」、自我介绍那句话
   - `assets/logo.svg`（网站标志）、`assets/avatar.svg`（头像，也是唱片中间那张）——换成 png / jpg 也行，改一下文件名
   - 「我的项目」里的三张示例卡：照着结构改文字、图标、按钮链接；不要的整块 `<article>` 删掉
   - 「联系我」里的 GitHub、邮箱
3. 直接用浏览器打开 `index.html` 就能看。放到任何静态托管上（GitHub Pages、Cloudflare Pages、自己的服务器）就上线了。

> 本地双击打开时，部分浏览器会拦截读取 JSON（状态卡显示页面里写死的数字）和歌词文件。用一个本地服务器打开就正常：`python -m http.server`，然后访问 http://localhost:8000 。

## 换歌和歌词

- 把你的歌放到 `assets/music/song.mp3`，再改 `index.html` 里播放器的歌名、歌手（搜 `晚风小调` 能找到三处）。
- 歌词用 LRC 格式（每行 `[分:秒.百分秒]歌词`），粘进 `index.html` 里 `<script type="text/plain" id="lrc-data">` 那一块；也可以清空那一块，放一个 `assets/music/song.lrc` 文件。
- **请只用你有权公开播放的音乐和歌词。** 模板自带的《晚风小调》是用代码合成的原创示例曲（拨弦琶音 + 垫音 + 轻鼓点），以 CC0 放弃版权，随便用。

## 实时状态卡

页面会读 `assets/demo/live.json`（每 60 秒）和 `assets/demo/stats.json`（打开页面时一次）：

```json
// live.json
{"online": true, "mood": "开心 80、专注 40", "doing": "在写代码", "doing_feel": "这次一定能跑通",
 "live_at": "2026-01-01 12:00:00", "ts": 1767240000}
```

```json
// stats.json：键名对应页面里的 data-dfy="..."
{"updated_at": "2026-01-01 12:00", "days_alive": 1, "groups_joined": 3, "people_known": 128,
 "group_messages_remembered": 2048, "tokens_total": 1000000}
```

`ts` 是 Unix 时间戳（秒），超过 10 分钟没更新就显示离线。让你的服务器用定时任务覆盖这两个文件就行。示例文件里带 `"demo": true`，不会被判成离线；正式用时去掉。

不需要状态卡的话，把那张卡里的 `<div class="live">…</div>` 删掉即可。

## 截图

放进卡片「展开」里的 `.shots`：

```html
<div class="shots">
  <a href="大图.jpg"><img src="缩略图.jpg" alt="说明" loading="lazy"><span>说明文字</span></a>
</div>
```

建议缩略图 640 像素宽、大图 1600 像素宽左右。示例截图来自开源项目 [小白标注](https://github.com/mengbaiyoudianxian/xiaobai-label)，图里的航拍图是公有领域 / CC0 图片。

## 许可（MIT + 署名条款，请务必看）

UI 来自 **孟白（https://mbclaw.top）**。免费使用、修改、商用都可以，但必须遵守 [LICENSE](LICENSE) 里的署名条款：

1. **每个公开页面的最下方**，必须保留一行清晰可见的署名「UI 来自 孟白 · mbclaw.top」，并且链接指向 https://mbclaw.top 。不能删除、隐藏、遮挡、改链接。模板里已经写好了（`index.html` 最底部的 `#ui-credit`），别动它就行；可以改颜色字号配合你的风格。
2. **改过之后再发布**（比如 fork 后改改再放到 GitHub），必须原样带上 LICENSE，在 README 里写明「UI 来自 孟白（https://mbclaw.top）」，保留页面署名，并要求再下游也这样做。
3. 违反署名条款，许可自动终止。

示例音乐《晚风小调》以 CC0 放弃版权；你换上去的音乐、歌词、图片的版权归各自的权利人。
