# BNI 華榮 121 會員資料｜Alice Tsai 蔡舜玉

單頁網站版 BNI 121 會員資料表。定位：**AI 商業流程架構師**。

基於 SBIR Phase 1 申請簡報重寫，把原本「機能服飾」定位轉為「把 AI 架構到品牌的商業流程上」。

## 本地預覽

```bash
open index.html
# 或
python3 -m http.server 8000 -d .
# 然後打開 http://localhost:8000
```

## 部署到 GitHub Pages

```bash
cd ~/bni-121-alice
git init
git add .
git commit -m "Initial BNI 121 page"
gh repo create bni-121-alice --public --source=. --push
# GitHub → Settings → Pages → Source: main / root
```

網址：https://roamingalice.github.io/bni-121-alice/

## 內容結構

| 區塊 | 對應 BNI 121 表單 |
|------|-------------------|
| Hero | 會員資料表開頭 |
| 商業 & 個人資訊 | 會員資料表 1、2 頁 |
| 強烈願望 & 秘密 & 成功關鍵 | 綜合資訊 |
| GAINS 工作表 | GAINS 5 大面向 |
| 目標客戶 & 引薦提示 | 最近 10 位客戶表 |
| 業務人脈圈 & 前三名 | 業務人脈圈 |

## 技術

- 單檔 HTML + 內聯 CSS
- Google Fonts: Noto Sans TC + Inter
- 無 build step、無 JS 依賴
- 響應式（手機／平板／桌面）
