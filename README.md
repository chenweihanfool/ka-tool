# 地籍圖整合工具

大湖地政事務所地籍資料轉換工具，將 COA / BNP / PAR / CTL 檔案輸出為 GeoJSON（EPSG:3826 TWD97）。

## 使用方式

1. 用 **Chrome 或 Edge** 開啟 `index.html`
2. 選擇包含各段子資料夾的頂層目錄（例如「115年5月」）
3. 勾選要輸出的項目
4. 按「開始處理」，完成後逐一下載 GeoJSON

## 輸出檔案

| 檔案 | 說明 |
|------|------|
| `界址點.geojson` | 界址點（Point），含段代碼、分幅、點號 |
| `宗地.geojson` | 宗地多邊形（Polygon），含段代碼、母號、子號、面積 |
| `圖根點.geojson` | 圖根點（Point），相同座標跨段合併，段代碼疊加 |

## 段代碼設定

「段代碼設定」頁可編輯各段的座標系統（twd67 / twd97），支援：
- 直接在表格內修改
- 匯出 / 匯入 CSV（`coord_system.csv`）
- 設定儲存於瀏覽器 localStorage

## 技術規格

- 純前端，無後端、無安裝
- 座標轉換：[proj4.js](https://github.com/proj4js/proj4js)（CDN）
  - TWD67 EPSG:3828 → TWD97 EPSG:3826
- 瀏覽器需求：Chrome / Edge（需 File System Access API）

## 檔案格式說明

**COA** — 界址點座標
```
12345 NNNNNNN.NNNNNNNNNEEEEEEE.EEEEEEEEE[flag]
```

**BNP** — 宗地邊界點序列
```
母號 子號 行號 總點數 點號1 點號2 ...
```

**PAR** — 宗地面積
```
母號 子號 code 面積(m²)
```

**CTL** — 圖根點
```
KAKxxxxxxxxx        ← 標頭（略過）
點名    NNNNNNN.NNNEEEEEE.EEE
```

## 版本紀錄

| 版本 | 日期 | 說明 |
|------|------|------|
| v1.0.0 | 2026-05-06 | 初始版本 |
