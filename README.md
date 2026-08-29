# Eishin's Interactive Resume | 繪本風格互動履歷

> 這是一份 RPG 風格冒險探索的互動式個人履歷網站。  
> 透過地圖探索、技能樹與職涯地標，以遊戲體驗的方式認識我的技術背景與實戰成果。

**[立即體驗](https://eishinchen.github.io/Resume/)**

---

## Tech Stack

| 領域 | 使用技術 |
| :--- | :--- |
| **Core Framework** | Vue 3 |
| **Build Tool** | Vite |
| **Styling & Layout** | CSS3 |
| **Deployment** | GitHub Pages + GitHub Actions |
| **Design Style** | Canva |

---

## Project Structure

```text
src/
├── assets/             # SVG 地圖、背景圖與全域樣式
├── components/         # 模組化組件
│   ├── AboutContent.vue        # 角色檔案
│   ├── SkillTreeContent.vue    # 技能樹
│   ├── ExperienceContent.vue   # 職涯足跡
│   ├── DetailModal.vue         # 動態彈出視窗
│   ├── StatusCard.vue          # 個人狀態面板
│   └── DialogBox.vue           # 角色對話框
├── views/
│   └── HomeView.vue            # 主地圖頁面
└── main.js
```
