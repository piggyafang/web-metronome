# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## 專案概述
這是一個純前端的網頁節拍器應用程式，由 NiceChord 好和弦開發。專案包含單一 HTML 檔案，使用 Web Audio API 實現音頻合成和節拍功能。

## 核心架構
- **單檔案應用程式**: 所有程式碼（HTML、CSS、JavaScript）都包含在 `index.html` 中
- **Web Audio API**: 使用瀏覽器原生音頻 API 進行音頻合成
- **即時音頻排程**: 採用預先排程機制確保精準的節拍時序

## 音頻技術規格
- **主拍音符**: C5 頻率 (523.25Hz)，音符長度 0.05 秒，音量 0.25
- **副拍音符**: G4 頻率 (392Hz)，音符長度 0.03 秒，音量 0.15
- **波形**: 方波振盪器 (square wave)
- **包絡線**: ADSR 衰減控制
- **排程參數**: 25ms lookahead，0.1s scheduleAheadTime

## 功能模組
### BPM 控制
- 範圍: 1-999 BPM
- 即時更新，按 Enter 鍵啟動

### 副拍系統
- 支援 0-1 之間的小數位置設定
- 逗號分隔多個副拍位置
- 預設快速設定：八分、三連音、十六分、附點、Swing 等

### 音頻排程器
- `scheduler()`: 主要排程迴圈
- `scheduleNote()`: 主拍音符排程
- `scheduleSubBeat()`: 副拍音符排程
- `nextBeat()`: 計算下一個音符時間

## 開發注意事項
- 無需建置工具，直接在瀏覽器中開啟 `index.html` 即可運行
- Web Audio API 需要使用者互動才能啟動（瀏覽器安全限制）
- 支援觸控裝置的 `ontouchend` 事件
- AudioContext 狀態管理（suspended/running）

## 測試方式
```bash
# 在本機開啟檔案
open index.html

# 或使用簡單 HTTP 伺服器
python3 -m http.server 8000
# 然後開啟 http://localhost:8000
```

## 相容性需求
- 現代瀏覽器支援 Web Audio API
- 支援 ES6+ JavaScript 語法
- 響應式設計適用於桌面和行動裝置