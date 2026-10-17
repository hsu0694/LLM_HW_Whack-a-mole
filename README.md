# LLM_HW_Whack-a-mole
### *** This is a small game, create by AI.   
### The prompt is from Gemini and the code is from Claude.

  
## Below is the original prompt from Gemini :   

### 專案名稱：打地鼠網頁遊戲 (Whack-a-Mole) 開發規格書
#### 1. 專案概述與技術棧
目標：開發一款具有現代可愛卡通風格的打地鼠網頁遊戲。

技術限制：必須使用純網頁技術 (Vanilla HTML, CSS, JavaScript)，不依賴任何前端框架（如 React, Vue）或編譯工具。程式碼需易讀，適合學術作業繳交。

跨裝置支援 (RWD)：遊戲必須支援響應式設計。無論在 Desktop、Tablet 還是 Mobile 上，版面都必須置中對齊，且 4x4 的地洞網格需自動適應螢幕寬度，確保不會破版。

#### 2. 遊戲核心機制
網格系統：4x4 配置，總共 16 個地洞。

遊戲時間：每局固定 40 秒。

地鼠種類與計分：

普通地鼠：打中 1 次即得分（+10 分），並觸發消失動畫。

鋼盔地鼠：需打中 2 次。

第 1 次打中：鋼盔掉落（發出金屬敲擊聲或改變圖片/樣式），不計分，地鼠不出洞。

第 2 次打中：成功擊暈（+20 分），並觸發消失動畫。

動態難度遞增 (Difficulty Curve)：

隨著剩餘時間減少，地鼠「探頭停留的時間」以及「下一次出現的間隔」必須越來越短。

例如：前 10 秒停留 1.2 秒，最後 10 秒可能只停留 0.7 秒。需在 JS 中動態計算。

##### 3. UI/UX 介面設計 (現代可愛卡通風)
整體視覺：背景可使用明亮的草地顏色，地洞要有陰影立體感，地鼠要有圓潤可愛的卡通感（可使用 CSS 繪製圓形/橢圓形加上表情，或預留清晰的圖片替換空間 <img>）。

資訊區塊 (Top/Side Bar)：

剩餘時間 (Time: 40s)

當前分數 (Score: 0)

最高分數 (High Score: 0) -> 必須使用 localStorage 儲存，讓網頁重整後依然保留最高分。

控制區塊：

「開始遊戲 (Start Game)」按鈕

「重新開始 (Restart)」按鈕 (遊戲進行中可重置)

#### 4. 動畫與視覺回饋 (CSS & JS)
地鼠進出動畫：利用 CSS overflow: hidden 與 transform: translateY() 達成從地洞中滑順探頭與縮回的動畫。

打擊回饋 (Hit Feedback)：

暈眩表情：成功擊中時，地鼠需切換至「暈眩（Dizzy）」樣式或圖片，停留 0.2 秒後再縮回。

飄動文字：擊中時，在游標/點擊位置動態生成一個 +10 或 +20 的 HTML 元素，向上飄動並淡出消失 (CSS @keyframes)。

螢幕震動：成功擊中時，透過對整個遊戲容器添加/移除 CSS class，產生短暫的微微震動效果。

#### 5. 音效 (Audio)
請在 HTML 中建立 <audio> 標籤，並在 JS 中設定觸發邏輯。

音效包含：

背景音樂 (BGM)：遊戲開始時循環播放，結束時停止。

打擊音效 (Hit Sound)：普通地鼠被擊中的聲音。

敲擊鋼盔音效 (Metal Sound)：打到鋼盔地鼠第一下的聲音。

遊戲結束音效 (Game Over)：時間歸零時播放。

(註：給 AI 的指示：請使用公開無版權的音效連結作為 placeholder，或使用 base64 寫入，方便我直接預覽測試。)

#### 6. 狀態管理 (JavaScript 邏輯重點)
使用 let timeUp = false; 來控制地鼠是否繼續出現。

需有效管理地鼠出現的定時器 (setTimeout / setInterval)，確保遊戲重置時能清除所有未完成的動畫和計時。

針對手機端，請確保點擊事件的靈敏度（可考慮綁定 mousedown 或 touchstart 減少延遲，並防止連點作弊機制 pointer-events: none）。

請根據以上規格，輸出結構清晰的 HTML、CSS (撰寫於 <style>)、JavaScript (撰寫於 <script>)。你可以將所有程式碼合併在一個 index.html 檔案中方便我測試。
