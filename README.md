







# MapleStory Reverse Engineering — Cosmic Control Panel (Demo)

> **這個 repo 只展示成果，不包含原始碼、不包含遊戲檔案。**
> This repository is a demo write-up only. No source code, binaries, or game assets are published.

個人的逆向工程與工具開發練習：為本機自架的 **Cosmic（GMS v83 私服模擬器）** 製作一個客戶端控制面板，研究遊戲客戶端與伺服器之間的互動方式。

A personal reverse-engineering side project: a control panel for a **locally hosted Cosmic (GMS v83) private-server emulator**, built to study how the game client and server interact.

---

## Demo


## 早期實驗影片 / Earlier experiment (2022)

2022 年在**本機自架私服**上錄製的早期實驗：調整角色攻擊參數、控制場景內怪物座標、擴大攻擊範圍。

An early 2022 experiment recorded on a **local, self-hosted private server**: tweaking character attack parameters, controlling in-map monster coordinates, and extending attack range.

https://github.com/user-attachments/assets/55413ab5-a3a2-47ff-9178-2076ed6ed2e3
## 逆向流程 / Reverse-engineering workflow

本專案的研究流程（為保護研究環境與避免被直接套用，**不公開任何位址、特徵碼或函式名稱**）。

The workflow behind this project. Addresses, byte signatures, and function names are intentionally not published.

```
 1. 取得乾淨映像        2. Memory dump          3. IDA Pro 靜態分析
    本機私服客戶端  ──►    已解殼的行程記憶體 ──►    反編譯 / 還原結構
                                                         │
 6. 自動化測試   ◄──  5. 掛鉤與驗證   ◄──  4. 執行期驗證 ◄┘
    假資料夾具          MinHook detour        觀察式 hook，只記錄不改動
```

1. **鎖定目標版本**：只針對本機私服使用的單一客戶端版本，記錄檔案雜湊與 PE 資訊（基底位址、映像大小、時間戳），之後所有分析都以此為準。
2. **Memory dump**：客戶端經過加殼，磁碟上的執行檔不能直接分析。待客戶端在**本機離線環境**完成解殼後，從行程記憶體傾印出已解殼的映像，作為分析素材。
3. **IDA Pro 靜態分析**：載入 dump，辨識函式邊界，用反編譯器還原偽 C，確認呼叫慣例與參數，並逐步還原物件結構與虛擬函式表，建立自己的函式與欄位命名。
4. **執行期驗證**：靜態分析的推論不直接當成事實。先用「只觀察、不修改」的 hook 記錄函式被呼叫時的參數與時機，與反編譯結果比對，確認理解正確。
5. **掛鉤與保護機制**：確認後才用 MinHook 實作 detour。每個 hook 安裝前都先驗證：檔案雜湊、模組基底、預期的原始位元組；任何一項不符就自動停用，不硬寫。支援一鍵全部停止與重啟式回復。
6. **自動化測試**：以假資料夾具與模擬的 hook 層測試邏輯，不啟動遊戲也能驗證狀態機、逾時與失效處理。

### 工具 / Tooling

IDA Pro（Hex-Rays）、x64dbg / 記憶體傾印工具、MinHook、C++ / C# / PowerShell。

### 心得 / Takeaways

- 解殼後的時機很重要：太早 patch 會破壞尚未解開的程式碼。
- 版本特定的假設一律寫成「驗證通過才啟用」，而不是直接相信位址。
- 先觀察、再修改：用觀察式 hook 的資料反證反編譯結果，避免憑猜測下手。

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

## 授權 / License

本頁內容與截圖為作者所有，保留所有權利。
Content and screenshots © the author. All rights reserved.
