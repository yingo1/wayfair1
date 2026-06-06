# Wayfair 展示页部署说明

## 上传到 GitHub Pages

把这些文件和文件夹上传到仓库根目录：

- `index.html`
- `admin.html`
- `site-data.js`
- `wayfair-reference.jpg`
- `assets/uploads/`

GitHub Pages 开启后，展示页入口是仓库 Pages 地址，后台入口是：

`/admin.html`

## 服务器端替换图片

线上页面会优先读取 `site-data.js` 里的图片路径。如果 `site-data.js` 里没有配置图片，才会读取浏览器后台本地保存的图片。

推荐把图片上传到：

- `assets/uploads/group1/`
- `assets/uploads/group2/`
- `assets/uploads/group3/`

然后在 `site-data.js` 中填写路径，例如：

```js
window.WAYFAIR_SITE_DATA = {
  group1: {
    main: [
      "assets/uploads/group1/main-1.jpg",
      "assets/uploads/group1/main-2.jpg",
      "assets/uploads/group1/main-3.jpg"
    ],
    specs: ["assets/uploads/group1/specs.jpg"],
    aplus: [
      "assets/uploads/group1/aplus-1.jpg",
      "assets/uploads/group1/aplus-2.jpg",
      "assets/uploads/group1/aplus-3.jpg",
      "assets/uploads/group1/aplus-4.jpg"
    ],
    purchase: [],
    compare: [],
    reviews: []
  },
  group2: { main: [], specs: [], aplus: [], purchase: [], compare: [], reviews: [] },
  group3: { main: [], specs: [], aplus: [], purchase: [], compare: [], reviews: [] }
};
```

各模块数量：

- `main`: 最多 10 张，前 3 张为主图展示，后 7 张为缩略图。
- `specs`: 1 张，点击 Specifications 后展示。
- `aplus`: 4 张，From the Brand 区域。
- `purchase`: 7 张，前 3 张为 Finish 小图，后 4 张为配件推荐。
- `compare`: 6 张，Compare Similar Items 的第 2-7 张；第 1 张自动使用 `main` 第 1 张。
- `reviews`: 7 张，前 5 张为评论区横排图，后 2 张为评论右侧图。

## 关于后台上传

`admin.html` 的上传功能保存到当前浏览器本地，适合临时预览。GitHub Pages 是静态网站，不能直接把后台上传的图片写入服务器文件。

如果要让所有访问者都看到同一套线上图片，请使用上面的 `assets/uploads/` + `site-data.js` 方式。
