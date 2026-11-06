







# MapleStory Reverse Engineering — (Demo)

> **這個 repo 只展示成果，不包含原始碼、不包含遊戲檔案。**
> This repository is a demo write-up only. No source code, binaries, or game assets are published.

個人的逆向工程與工具開發練習：為本機自架的 **私服模擬器**，研究遊戲客戶端與伺服器之間的互動方式。

A personal reverse-engineering side project

---

## Demo


## Earlier experiment (2022)

2022 年在**本機自架私服**上錄製的早期實驗：調整角色攻擊參數、控制場景內怪物座標、擴大攻擊範圍。

An early 2022 experiment recorded on a **local, self-hosted private server**: tweaking character attack parameters, controlling in-map monster coordinates, and extending attack range.

https://github.com/user-attachments/assets/55413ab5-a3a2-47ff-9178-2076ed6ed2e3

## 2026 後續用Agent完成加速、飛行等功能 


https://github.com/user-attachments/assets/4212c6c3-4339-4e40-bb03-f0f515f1fd40

## 逆向流程 / Reverse-engineering workflow


1. **Memory dump**：客戶端經過加殼，執行檔無法直接做靜態分析。因此先執行客戶端，在記憶體中解殼後，再從記憶體 dump 出來。
2. **動態分析**：用 Cheat Engine 找出可能的 function 位址。但 Cheat Engine 只顯示 x86 assembly，可讀性很低，所以後續改用 IDA Pro 分析程式邏輯。
3. **IDA Pro 靜態分析**：載入 dump，閱讀可讀性更高的反編譯程式碼。
4. **Client patch**：使用 Cheat Engine 動態 patch client，達成調整角色攻擊參數、控制場景內怪物座標、擴大攻擊範圍等行為。


## Disclaimer

- 僅用於**本機、離線、自己架設的模擬器**環境。

---
