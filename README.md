# 米哈游.com · 抽卡跳转站

[![给我点个 Star 谢谢喵](star.png)](https://github.com/longking2012/mihuyou/stargazers)

> 打开就抽一发，抽到哪张卡，就跳哪个网址。

## 这是什么

一个网页整活项目。每次访问首页，页面会模拟二游「抽卡」动画随机抽一张卡，根据抽到的卡把浏览器跳转到对应的网址。所有跳转链接都集中在脚本里，改起来很方便。

## 功能特性

- 还原二游抽卡机制：限定 UP、大小保底、软硬保底、捕获明光、mulberry32 伪随机
- 抽卡动画 + 结果展示 + 自动跳转
- 附带站内搜索页（Bing 跳转）

## 文件结构

```
米哈游.com/
├── index.html          # 主页入口，加载 aha.js
├── aha.js              # 反混淆后的工作源码（947 行，可直接阅读/修改）
├── star.png            # 「求个 Star」引导图
├── .github/workflows/
│   └── snapshot.yml    # 每小时云端抓取 aha.js 并归档旧版（GitHub Actions）
├── baseline/           # 抓取对比基准，由 Actions 自动维护（勿手改）
├── old/                # aha.js 历史旧版自动存档，由 Actions 生成
├── sarach/             # 站内搜索页「感觉都不如原神」
│   ├── 感觉都不如原神.html
│   └── 感觉都不如原神_files/
├── 原版/               # 最初从网站抓取的原始文件存档（对照用，站点运行不依赖）
│   ├── aha.js          # 原始混淆壳（eval + base64 + xor 自解码）
│   ├── aha.js.下载     # 同名混淆壳，带中文后缀
│   ├── aha.decoded.js  # 解混淆后的干净源码（与根目录 aha.js 同源）
│   ├── 米哈游.com.html # 原始主页（引用 aha.js.下载）
│   └── sarach/         # 原始搜索页存档
└── README.md
```

## 自定义链接

打开 `aha.js`，只要改两个地方：

- `GROUPS` —— 限定卡池（5★ UP、常驻等）
- `FILLER_GROUPS` —— 填充卡池（3★ 狗粮等）

每个分组形如：

```js
{
  name: '3星狗粮',
  urls: [
    'https://www.qq.com/',
    'https://space.bilibili.com/325534942', // Longking2012 的 B站主页
    // ...
  ]
}
```

往 `urls` 数组里加你想跳转的网址即可。

> 注：根目录 `aha.js` 已把本人 B站（`https://space.bilibili.com/325534942`）加入「3星狗粮」分组，并把搜索页路径从失效的 `./search.html` 修正为 `./sarach/感觉都不如原神.html`。

## 本地预览

直接用浏览器打开 `index.html` 即可，无需服务器。

## 部署（GitHub Pages）

1. 把本仓库推到 GitHub（建议仓库名 `mihayo-com`）
2. 仓库 **Settings → Pages → Source** 选 `main` 分支、根目录 `/`
3. 稍等片刻，Pages 地址即生效

## 自动归档 aha.js（GitHub Actions）

`.github/workflows/snapshot.yml` 会在 GitHub 云端**每小时**（以及 `aha.js` 一有更新时）自动：

1. 抓取线上 `aha.js`；
2. 与 `baseline/aha.js`（上次抓到的基准）对比；
3. 一旦发现变化，就把旧版存到 `old/aha_时间戳.js`，并更新基准与根目录脚本。

全程在 GitHub 服务器上完成，**本地不需要运行任何脚本、不产生任何文件**。也可在仓库 **Actions** 页面手动触发。

## 版权与所有权

- 本仓库内容抓取并反编译自 **米哈游.com**，原作者为米哈游.com；本人（Longking2012）并非原作者，仅作存档、学习与部署之用，**所有权归米哈游.com 所有**。
- 本人 B站：[@Longking2012](https://space.bilibili.com/325534942)

## 说明

- 本项目为个人整活 / 学习用途，跳转目标均为公开网站。
- `原版/` 目录仅作抓取存档与对照，站点运行不依赖它。
