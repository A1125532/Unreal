# Mygame3 專案說明

本專案為 Unreal Engine 4.27 專案，使用 DMX（Art-Net）相關插件進行燈光控制與舞台場景內容製作。  
目前專案以 Blueprint/資產為主。

完整檔案：https://drive.google.com/drive/folders/12-IquzWPvdQjNdV0deGNnTJachwU9jls?usp=sharing

---

## 1. 專案基本資訊

- **專案名稱**：`Mygame3`
- **引擎版本**：`Unreal Engine 4.27`（來自 `Mygame3.uproject` 的 `EngineAssociation`）
- **主要技術方向**：
  - DMX / Art-Net 通訊
  - 舞台燈光與場景資產
  - Unreal 內建 Template + StarterContent 延伸
- **程式架構型態**：目前為「無 C++ Source 資料夾」的內容導向專案

---

## 2. 目錄結構與用途

專案根目錄主要結構如下：

- `Mygame3.uproject`：專案入口檔與插件啟用設定
- `Config/`：專案預設設定（地圖、渲染、DMX、輸入等）
- `Content/`：所有 Unreal 資產（場景、藍圖、材質、貼圖、地圖等）
- `DerivedDataCache/`：快取資料（可重建）
- `Intermediate/`：中間產物（可重建）
- `Saved/`：執行/編輯器輸出（Log、使用者本機設定等）
- `Script/`：目前存在但內容為空

---

## 3. 主要設定檔說明

### 3.1 `Config/DefaultEngine.ini`

#### (A) 預設地圖

- `EditorStartupMap=/Game/DMXTemplate/Maps/Fixtures.Fixtures`
- `GameDefaultMap=/Game/DMXTemplate/Maps/Fixtures.Fixtures`

代表編輯器啟動與遊戲執行都會優先進入 `Fixtures` 地圖。

#### (B) 渲染相關

目前可確認的重要項目：

- `r.AllowStaticLighting=False`
- `r.SSGI.Enable=True`
- `r.AllowGlobalClipPlane=True`
- Auto Exposure / Bloom / Lens Flare 啟用

#### (C) DMX / Art-Net 設定

在 `[/Script/DMXProtocol.DMXProtocolSettings]` 定義了 3 組 Input 與 3 組 Output Port：

| 類型 | Port 名稱 | Protocol | 通訊模式 | Universe 範圍 |
|---|---|---|---|---|
| Input | InputA | Art-Net | InternalOnly | Local 1~5（Extern 1~5） |
| Input | InputB | Art-Net | InternalOnly | Local 7（Extern 7） |
| Input | InputC | Art-Net | InternalOnly | Local 6（Extern 6） |
| Output | OutputA | Art-Net | Broadcast | Local 1~5（Extern 1~5） |
| Output | OutputB | Art-Net | Broadcast | Local 7（Extern 7） |
| Output | OutputC | Art-Net | Broadcast | Local 6（Extern 6） |

其他重點：

- `SendingRefreshRate=30`
- `bDefaultSendDMXEnabled=True`
- `bDefaultReceiveDMXEnabled=True`

#### (D) 遊戲名稱導向

- `TP_DMXBP` 相關名稱被重導向到 `/Script/Mygame3`，表示專案源自 DMX Blueprint Template 並已更名。

### 3.2 `Config/DefaultGame.ini`

- 啟用 StarterContent pack 插入動作：
  - `bAddPacks=True`
  - `InsertPack=(PackSource="StarterContent.upack",PackName="StarterContent")`

### 3.3 `Config/DefaultInput.ini`

- `bAlwaysShowTouchInterface=False`
- 目前未看到自訂 Action/Axis 綁定條目

### 3.4 `Config/DefaultEditor.ini`

- 目前檔案內容為空（保留預設狀態）

---

## 4. 插件狀態（`Mygame3.uproject`）

### 已啟用

- `DMXProtocol`
- `DMXEngine`
- `DMXFixtures`
- `DMXPixelMapping`
- `ModelingToolsEditorMode`
- `StaticMeshEditorExtension`

### 已停用

- `OculusVR`（Win32 / Win64）
- `SteamVR`（Win32 / Win64）
