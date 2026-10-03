# 嘟嚕與啵啵 Dulu & Bobo

兩隻住在 Windows 桌面上的 3D 果凍小夥伴。可以戳、拖、甩，牠們會壓扁、回彈、互相擠來擠去，各自可以換六種口味。這是一款給 [Lively Wallpaper](https://github.com/rocksdanister/lively) 用的網頁動態桌布。

---

## 1. 這個專案解決什麼問題

一般的動態桌布只能看，不能玩。這個專案讓桌面本身變成一個可以摸的小玩具：工作累了，把視窗縮小，戳一下果凍、把牠丟出去，看牠彈回來，就能放鬆一下。

另外幾個設計目標：

- **不用連網**：3D 引擎（three.js）放在資料夾裡，斷網也能跑。
- **不用寫程式**：口味、隻數、自動換色等設定，都能在 Lively 的「自訂」面板裡用下拉選單調整。
- **不擋桌面**：文字和按鈕都放在畫面右側，避開左邊的桌面圖示和下方的工作列。

## 2. 主要功能

| 分類 | 功能 |
| --- | --- |
| 角色 | 兩隻果凍：**嘟嚕**（預設汽水藍）和**啵啵**（預設草莓粉），可以切成只顯示 1 隻 |
| 物理 | 軟體物理（shape matching）：會被拉長、落地壓扁再回彈，會自己慢慢站正；兩隻會互相碰撞、擠開 |
| 表情 | 平常是圓點眼、會隨機眨眼，眼睛會跟著滑鼠看；被戳變 `> <`，拖著時瞇眼，在空中變 `O` 嘴驚訝，重重落地會暈眩（漩渦眼），被摸會變愛心眼 |
| 口味 | 汽水、草莓、青蘋果、芒果、葡萄、極光（極光是乳白色加彩虹光澤） |
| 計數 | 右上角「Q彈」計數器：每次戳、摸到冒愛心、丟出去落地都會 +1 |
| 音效 | 用 Web Audio 即時合成的「啵～」彈跳聲，兩隻的音高不同；預設關閉 |
| 自動換色 | 可設定每 1 / 5 / 15 / 30 / 60 分鐘自動換一次口味 |
| 記憶 | 用瀏覽器的 localStorage 記住兩隻上次選的口味 |

## 3. 安裝方法

### 系統需求

- Windows 10 / 11
- [Lively Wallpaper](https://github.com/rocksdanister/lively)（免費，可從 Microsoft Store 安裝）
- 支援 WebGL 的顯示卡（近幾年的內顯也可以）

### 步驟

1. 從 Microsoft Store 搜尋並安裝 **Lively Wallpaper**。
2. 到 [Releases](https://github.com/POUND0423/Cute-Slime-3D/releases) 下載最新的 `Cute-Slime-3D-v版本.zip`（例如 `Cute-Slime-3D-v0.1.0.zip`）。也可以自己把 `index.html`、`three.min.js`、`LivelyInfo.json`、`LivelyProperties.json`、`project.json` 打包成 zip。
3. 打開 Lively，把 zip 拖進桌布清單（或按右上角的 **＋** 選擇檔案）。
4. 在清單中點選「**嘟嚕與啵啵**」套用。
5. 按 **Windows 鍵 + D** 回到桌面。

> 如果之前裝過舊版的「嘟嚕 Dulu」，請先在 Lively 清單裡刪除，避免選錯。

### 使用 Wallpaper Engine（未實測）

資料夾內附 `project.json`，格式依照 Wallpaper Engine 網頁桌布的規格撰寫，可以用「開啟壁紙 → 從檔案開啟」選 `index.html` 匯入。目前只在 Lively 的規格下開發與測試，Wallpaper Engine 上的表現尚未驗證。

### 檔案結構

```
dulu-wallpaper/
├── index.html              主程式（畫面、物理、互動、設定接收）
├── three.min.js            three.js r149（3D 引擎，離線使用）
├── LivelyInfo.json         Lively 桌布資訊（名稱、類型 Type=1 網頁）
├── LivelyProperties.json   Lively「自訂」面板的設定項目
├── project.json            Wallpaper Engine 用的設定描述
├── README.md               本文件
└── LICENSE                 MIT 授權
```

## 4. 使用方法

### 滑鼠操作

| 操作 | 效果 |
| --- | --- |
| 按住果凍拖曳 | 抓著走，身體會被拉長；放開時有速度就會被甩出去 |
| 快速點一下果凍（移動不到 5px、按住不到 0.4 秒） | 戳戳：被點的地方凹進去、小跳一下、表情變 `> <` |
| 滑鼠在果凍上來回移動（不按） | 摸摸：累積夠了會變愛心眼並冒出愛心 |
| 在果凍上滾滾輪 | 往下滾壓扁、往上滾拉高，放開後慢慢恢復 |
| 觸控板雙指縮放（Ctrl + 滾輪） | 捏捏：拉開變扁、捏合變高 |
| 觸控螢幕雙指 | 拉開變扁、捏合變高（作用在目前選取的那隻） |
| 把一隻甩向另一隻 | 兩隻會碰撞、擠開 |

> 在 Lively 裡要能戳到果凍，請確認 Lively 設定中的 **Wallpaper Input** 設為 **Mouse**。

### 換口味（桌布上）

1. 點右下角的「**嘟嚕**」或「**啵啵**」小按鈕，選擇要換的那隻。直接戳或拖某一隻也會自動選到牠。
2. 點下面六顆口味按鈕之一。

標題的「Q彈Q彈。」顏色會跟著目前選取那隻的口味變。

### Lively「自訂」面板

在 Lively 清單中的桌布上按右鍵 →「自訂」（Customize）：

| 設定 | 選項 | 預設 |
| --- | --- | --- |
| 幾隻 | 1 隻 / 2 隻 | 2 隻 |
| 嘟嚕的口味 | 汽水、草莓、青蘋果、芒果、葡萄、極光 | 汽水 |
| 啵啵的口味 | 同上 | 草莓 |
| 自動換口味 | 不要 / 每 1、5、15、30 分鐘 / 每 1 小時 | 不要 |
| 顯示標題文字 | 開 / 關 | 開 |
| 顯示口味按鈕 | 開 / 關 | 開 |
| 顯示 Q彈 次數 | 開 / 關 | 開 |
| 音效 | 開 / 關 | 關 |

說明：

- 自動換口味時，每次嘟嚕往後換 1 種、啵啵往後換 2 種，所以兩隻不會一直同色。
- Lively 每次啟動都會把面板裡的設定送進來，所以重開機後會套用面板上選的口味。想固定口味，建議在面板裡設定。

## 5. 輸入輸出範例

### 範例 A：滑鼠互動

| 輸入 | 輸出 |
| --- | --- |
| 在嘟嚕身上快速點一下 | 嘟嚕被點的地方凹陷、彈跳一下，表情 `> <` 約 0.65 秒；Q彈計數 +1；約三分之一機率冒出 3 顆愛心 |
| 抓住啵啵往上甩後放開 | 啵啵飛起並露出驚訝臉；落地時壓扁回彈並變開心臉（`^ ^`），Q彈計數 +1；落地太用力會變漩渦眼 |
| 滑鼠在嘟嚕身上來回晃 | 嘟嚕變愛心眼約 1.6 秒、冒出 5 顆愛心、身體扭一下，Q彈計數 +1 |
| 點「啵啵」再點「葡萄」 | 啵啵在約半秒內漸變成紫色，開心地跳一下；標題文字變紫色 |

### 範例 B：Lively 設定 → 桌布反應

Lively 透過 `livelyPropertyListener(名稱, 值)` 把設定傳進頁面，下拉選單傳的是選項的索引（從 0 開始）：

```js
livelyPropertyListener('flavor2', 4);   // 啵啵 → 葡萄（第 5 個選項）
livelyPropertyListener('count', 0);     // 只留嘟嚕，啵啵消失
livelyPropertyListener('count', 1);     // 啵啵從上方掉回來
livelyPropertyListener('cycle', 2);     // 每 5 分鐘自動換口味
livelyPropertyListener('showText', false); // 隱藏右側標題文字
livelyPropertyListener('sound', true);  // 打開音效
```

### 範例 C：`LivelyProperties.json` 片段

```json
"flavor1": {
  "type": "dropdown",
  "value": 0,
  "text": "嘟嚕的口味",
  "items": ["汽水（藍）", "草莓（粉紅）", "青蘋果（綠）", "芒果（黃）", "葡萄（紫）", "極光（彩虹白）"]
}
```

`value` 改成 `5`，嘟嚕預設就會是極光口味。

## 常見問題

| 狀況 | 原因與處理 |
| --- | --- |
| 畫面只有一行「嘟嚕還沒載入」 | 找不到 `three.min.js`，或顯示卡不支援 WebGL。確認 `three.min.js` 和 `index.html` 在同一個資料夾；本機找不到時，程式會依序改從 jsDelivr、unpkg、cdnjs 下載，但這需要連網 |
| 果凍戳不動 | Lively 設定 → Wallpaper Input 改成 Mouse；並確認滑鼠點的是桌面空白處，不是圖示或視窗 |
| 字型和截圖不一樣 | 標題字型（粉圓 Huninn、Noto Sans TC、Fraunces）從 Google Fonts 載入，離線時會改用系統字型（微軟正黑體），功能不受影響 |
| 擔心吃效能 | 開全螢幕程式時 Lively 會自動暫停桌布；畫面同一時間只算兩隻果凍，每隻約 640 個頂點 |

## 技術說明

- **3D**：three.js r149，`MeshPhysicalMaterial`（transmission、clearcoat；極光口味加 iridescence 和 sheen），自製 HDR 環境光與大理石地板貼圖。
- **物理**：每隻果凍是一顆約 640 個質點的球形網格，每秒以 240 步做 position-based shape matching：旋轉部分用 Müller 等人（2016）的迭代法求得，再混入 28% 的線性形變讓它更 Q。地板有摩擦，兩隻之間用橢球推開來處理碰撞。
- **表情**：每隻各有一張 512×512 的 canvas，畫好臉後當貼圖貼在身體正面；眼睛看滑鼠的效果是靠位移貼圖做出來的。
- **設定介面**：同時支援 Lively（`livelyPropertyListener`）和 Wallpaper Engine（`wallpaperPropertyListener`）。三維引擎載入前送來的設定會先排隊，載入後再套用。

## 授權

本專案以 [MIT License](LICENSE) 釋出。

內附的 `three.min.js` 屬於 three.js，同樣採用 MIT 授權，版權屬於 three.js authors。
