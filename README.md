



# MapleStory Reverse Engineering — Cosmic Control Panel (Demo)

> **這個 repo 只展示成果，不包含原始碼、不包含遊戲檔案。**
> This repository is a demo write-up only. No source code, binaries, or game assets are published.

個人的逆向工程與工具開發練習：為本機自架的 **Cosmic（GMS v83 私服模擬器）** 製作一個客戶端控制面板，研究遊戲客戶端與伺服器之間的互動方式。

A personal reverse-engineering side project: a control panel for a **locally hosted Cosmic (GMS v83) private-server emulator**, built to study how the game client and server interact.

---

## ⚠️ 範圍與免責 / Scope & Disclaimer

- 僅用於**本機、離線、自己架設的 v83 模擬器**環境。
- **不是**給官方 / 商業營運伺服器使用的工具，也請勿用於官方伺服器。
- 本 repo 不含 `MapleStory.exe`、DLL、`.wz` 或任何受著作權保護的遊戲素材。
- 原始碼不公開，因此也不提供下載、建置或使用說明。
- 「MapleStory」及相關名稱屬於其權利人，本專案與其無任何關聯，亦未獲授權。

- For a **local, offline, self-hosted v83 emulator** only.
- **Not** intended for, and should never be used on, official or commercial servers.
- No game executables, DLLs, `.wz` files, or other copyrighted assets are included.
- Source code is not published, so there are no build or usage instructions.
- "MapleStory" and related names belong to their respective owners; this project is unaffiliated and unauthorized.

---

## Demo


## 早期實驗影片 / Earlier experiment (2022)

2022 年在**本機自架私服**上錄製的早期實驗：調整角色攻擊參數、控制場景內怪物座標、擴大攻擊範圍。

An early 2022 experiment recorded on a **local, self-hosted private server**: tweaking character attack parameters, controlling in-map monster coordinates, and extending attack range.
https://github.com/user-attachments/assets/d79a3f54-7af5-4031-bad9-7f191c8201e3

## 架構 / Architecture

```
┌──────────────────────────────────────┐
│  C# WinForms 桌面面板                 │
│  即時狀態顯示、設定、一鍵全部停止      │
└───────────────────┬──────────────────┘
                    │ JSON / 行程協調
┌───────────────────▼──────────────────┐
│  PowerShell 設定與狀態驗證層          │
└───────────────────┬──────────────────┘
                    │ 本機 IPC
┌───────────────────▼──────────────────┐
│  C++ 客戶端模組（MinHook）            │
└──────────────────────────────────────┘
```

## 技術重點 / What I worked on

- C# WinForms 面板：High-DPI、深色主題、即時狀態回報、「全部停止」安全開關
- 面板與模組之間的狀態驗證與逾時 / 失效處理
- 以 MinHook 對本機客戶端做函式掛鉤的研究與測試
- 自動化測試與建置腳本

## 授權 / License

本頁內容與截圖為作者所有，保留所有權利。
Content and screenshots © the author. All rights reserved.
