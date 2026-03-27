# 💰 理財生存戰 — 金融教育遊戲套件

> 青溪國小親職教育日 — 金融教育互動遊戲

## 🎮 遊戲總覽

本專案包含三款金融教育遊戲與即時連線系統，專為國小學生設計，讓孩子透過遊戲體驗理財、投資與風險管理。

| 檔案 | 說明 | 連結 |
|------|------|------|
| `finance-games.html` | 遊戲大廳（入口頁面） | [開啟](https://gn00318361-collab.github.io/money-game/finance-games.html) |
| `moneygame.html` | 🎲 理財生存戰（骰子版） | [開啟](https://gn00318361-collab.github.io/money-game/moneygame.html) |
| `monetgame.html` | 📈 金融生存戰（股市版） | [開啟](https://gn00318361-collab.github.io/money-game/monetgame.html) |
| `leaderboard.html` | 🏆 即時排行榜 | [開啟](https://gn00318361-collab.github.io/money-game/leaderboard.html) |
| `admin.html` | 🛑 老師控制台 | [開啟](https://gn00318361-collab.github.io/money-game/admin.html) |

---

## 🎲 理財生存戰（骰子版）`moneygame.html`

擲骰子決定命運的理財模擬遊戲，12 個月內累積資產達到 $200,000 即可過關。

**玩法：**
選擇職業（外送員 / 行政員 / 工程師），每月擲骰子執行行動（工作、進修、投資、放鬆），骰子結果決定收入與事件。壓力爆表（100%）或破產（餘額 < 0）= 立即 GAME OVER。

**特色：** 3D 骰子動畫、死亡機制（破產/過勞）、全螢幕勝負畫面、Google Sheets 自動記錄成績。

---

## 📈 金融生存戰（股市版）`monetgame.html`

在黑天鵝事件中活下來，撐過 10 輪不破產！

**玩法：**
起始資金 $1,000，每 10 秒觸發一次黑天鵝事件（地震、戰爭、疫情、央行升息等 12 種），買賣三種資產（科技股、能源股、黃金）來分散風險，資產淨值歸零即破產。

**特色：** Firebase 即時連線（分數同步至排行榜）、老師可遠端觸發市場崩盤、Google Sheets 成績記錄。

---

## 🏆 即時排行榜 `leaderboard.html`

Firebase 即時同步的全班排行榜，投影到大螢幕讓全班觀戰。

**功能：** 線上人數統計、最高分顯示、破產人數、獎牌標示（🥇🥈🥉）、排名升降箭頭、線上/離線狀態（綠點/灰點）、破產玩家顯示 💀、老師事件橫幅閃爍提示。

---

## 🛑 老師控制台 `admin.html`

老師專用面板，可即時發動全域市場事件影響所有正在遊戲的學生。

**事件按鈕：**
- 科技崩盤（科技股 -50%）
- 能源危機（能源股 -60%）
- 現金貶值（現金 -30%）
- 重置所有玩家資料

---

## 🔗 連線架構

三個頁面（monetgame、leaderboard、admin）共用同一個 Firebase Realtime Database：

```
Firebase DB
├── players/{玩家名稱}    ← monetgame 寫入，leaderboard 讀取
│   ├── score            ← 即時淨值
│   └── lastUpdate       ← 時間戳（判斷在線）
└── global_event         ← admin 寫入，monetgame + leaderboard 讀取
    ├── id               ← 事件 ID
    ├── target           ← 影響目標
    ├── impact           ← 影響倍率
    └── msg              ← 顯示訊息
```

---

## 📋 成績記錄（Google Sheets）

兩款遊戲結束時自動透過 Google Apps Script 將成績寫入 Google Sheets，欄位包含：時間、玩家、遊戲名稱、星等、結果摘要、關鍵數值等。Apps Script 原始碼見 `google-apps-script.txt`。

---

## 🚀 使用方式

1. 打開 `finance-games.html` 作為遊戲大廳入口
2. 老師另開 `admin.html` 控制市場事件
3. 投影 `leaderboard.html` 到教室大螢幕
4. 學生用手機或平板開啟遊戲

無需安裝任何套件，純前端 HTML + CSS + JavaScript + Firebase CDN。

---

## 📋 適用對象

- 國小中高年級學生
- 親職教育日課程活動
- 金融素養教學輔助教材

## 🛠️ 技術

HTML / CSS / JavaScript / Tailwind CSS (CDN) / Firebase Realtime Database (compat v9.15.0) / Google Apps Script
