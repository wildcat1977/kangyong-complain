# 康永哥告狀器

做「康熙來了」風格告狀康永哥梗圖的小工具。上傳人物照片、自動去背、填兩段字，就能下載 PNG。

所有處理都在瀏覽器裡完成，照片不會上傳到任何伺服器。

## 功能

- 人物：可選預設人物（`presets/`，已去背），或上傳照片後自動去背；在圖上拖曳移動，滾輪或雙指縮放，也能左右翻轉。
- 大字第一行：用 `[ ]` 框起來的字會變成放大的藍色重點字，例如 `他叫我[搭機捷]欸`。
- 大字第二行：預設「康永哥」。
- Q 標籤：兩行紅字。

## 技術

- 單一靜態頁面 `index.html`，沒有建置步驟，用 Canvas 合成圖片。
- 去背使用 [IMG.LY background-removal](https://github.com/imgly/background-removal-js) 1.7.0（`isnet_quint8` 模型），模型與 wasm 從 IMG.LY 的 CDN 載入，第一次約 56MB，之後由瀏覽器快取。
- 字型使用 Google Fonts 的 Noto Sans TC。
- 預設人物用 `@imgly/background-removal-node`（medium 模型）先去背，裁到主體後轉成 WebP（本圖高 1000px 以內，`_thumb` 為 180px 縮圖）。新增人物：放入 `presets/<file>.webp` 與 `presets/<file>_thumb.webp`，並在 `index.html` 的 `PRESETS` 加一筆。

本機測試：

```sh
python3 -m http.server 8765
```

## 授權

AGPL-3.0，與所使用的 IMG.LY background-removal 相同。見 [LICENSE.md](LICENSE.md)。

底圖 `bg.jpg` 為重新生成的仿節目場景圖。
