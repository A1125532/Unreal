# 找蘑菇遊戲（MyGame）

這是一個使用 **Unreal Engine 4.27** 製作的第三人稱尋找物件遊戲專案，核心玩法是玩家在場景中移動並尋找指定蘑菇目標。  
專案以 Blueprint 與美術資產為主。

完整檔案：https://drive.google.com/drive/folders/1vMobOm9sl__H0-VUCQFiZMthLusL6u-p?usp=drive_link

---

## 1) 專案基本資訊

- 專案名稱：`MyGame`
- 引擎版本：`UE 4.27`（`MyGame.uproject`）
- 預設啟動地圖：`/Game/003_menu/main_menu`
- 預設 GameMode：`/Game/ThirdPersonBP/Blueprints/ThirdPersonGameMode`
- 專案型態：第三人稱 Blueprint 專案（基於 Third Person BP Template）

---

## 2) 遊戲定位與玩法說明（找蘑菇）

依據目前資產命名、關卡流與執行紀錄可推定，本遊戲流程為：

1. 進入主選單 `main_menu`
2. 點擊開始後進入遊玩關卡 `ThirdPersonExampleMap`
3. 達成條件後切換到結算/次畫面 `Second`

### 玩法核心

- 玩家以第三人稱角色在場景中探索。
- 目標物件為紅色蘑菇（資產：`/Game/003_menu/Red_Mushroom`，並有 `001-MyGame/Model/Mushroom` 模型素材）。
- UI 包含主選單與結束介面（`main_menu_interface`、`main_menu_interface_ending`、`scond_interface_ending`）。

> 註：由於 Blueprint/UMAP 為二進位資產，無法直接以文字反編譯邏輯；README 內容是依「地圖切換紀錄 + 資產命名 + 設定檔」整理出的可靠推論。

---

## 3) 關卡與流程

### 主要關卡檔案

- `Content/003_menu/main_menu.umap`：主選單
- `Content/003_menu/ThirdPersonExampleMap.umap`：主要遊玩場景
- `Content/003_menu/Second.umap`：結束/次畫面
- `Content/001-MyGame/MyGame_Map.umap`：舊版或測試地圖
- `Content/003_menu/MyGame_Map.umap`：同名地圖版本（可能為備份/分支）

### 實際執行紀錄中的切圖順序

在打包執行日誌可見：

1. `LoadMap: /Game/003_menu/main_menu`
2. `LoadMap: /Game/003_menu/ThirdPersonExampleMap`
3. `LoadMap: /Game/003_menu/Second`

此流程與「主選單 -> 遊戲中 -> 結束畫面」結構一致。

---

## 4) 操作方式

根據 `Config/DefaultInput.ini`：

- `W / A / S / D`：移動
- 滑鼠移動：視角控制
- `Space`：跳躍
- `R`：ResetVR（VR 視角重置）

---

## 5) 目錄結構（重點導覽）

```text
MyGame/
├─ MyGame.uproject
├─ Config/                       # 專案設定（地圖、輸入、引擎）
├─ Content/
│  ├─ 001-MyGame/                # 自製素材與地圖（大量模型）
│  │  ├─ Model/
│  │  │  ├─ Mushroom/            # 蘑菇模型素材
│  │  │  ├─ Car, JapanCar...     # 車輛模型庫
│  │  └─ MyGame_Map.umap
│  ├─ 003_menu/                  # 遊戲實際流程主資料夾
│  │  ├─ main_menu.umap
│  │  ├─ ThirdPersonExampleMap.umap
│  │  ├─ Second.umap
│  │  ├─ main_menu_interface.uasset
│  │  ├─ main_menu_interface_ending.uasset
│  │  ├─ scond_interface_ending.uasset
│  │  └─ Red_Mushroom.uasset
│  ├─ ThirdPersonBP/             # 第三人稱範本藍圖
│  └─ StarterContent/            # UE 內建素材
├─ Build/                        # 打包輸出相關
├─ Intermediate/                 # UE 暫存中介檔
├─ Saved/                        # 日誌、快取、Cooked 資料
├─ Model/                        # 專案外部模型來源資料
└─ （另有一份 WindowsNoEditor 打包輸出資料夾）
```

