<template>
  <div class="skill-split-layout">
    <!-- 左半邊：實戰作品展示卡 (占比約 45%) -->
    <div class="project-panel">
      <div class="panel-title">
        <span>實戰作品成果</span>
        <span class="active-tech-badge">{{ selectedSkill.name }}</span>
      </div>

      <div v-if="selectedSkill.project" class="project-content">
        <h4 class="project-name">{{ selectedSkill.project.title }}</h4>
        <p class="project-desc">{{ selectedSkill.project.desc }}</p>

        <!-- 連結按鈕區 -->
        <div class="project-links">
          <a
            v-if="selectedSkill.project.demoUrl"
            :href="selectedSkill.project.demoUrl"
            target="_blank"
            class="doodle-btn"
          >
            🚀 Demo
          </a>
          <a
            v-if="selectedSkill.project.githubUrl"
            :href="selectedSkill.project.githubUrl"
            target="_blank"
            class="doodle-btn outline"
          >
            📦 GitHub
          </a>
        </div>
      </div>

      <!-- 如果點到的技能尚未綁定作品，顯示圖片與提示 -->
      <div v-else class="empty-project">
        <img src="@/assets/empty-box.svg" alt="No Projects" class="empty-img" />
        <p class="empty-text">
          目前尚無公開的展示作品<br />
          <span class="empty-subtext">相關技術主要應用於內部系統開發或資料庫維護</span>
        </p>
      </div>
    </div>

    <!-- 右半邊：技能樹 SVG 地圖 (占比約 55%) -->
    <div class="tree-panel">
      <div class="skill-board">
        <img src="@/assets/skill-tree-bg.svg" class="skill-svg-bg" alt="Skill Tree" />

        <!-- 標籤點位 -->
        <div
          v-for="skill in skillList"
          :key="skill.name"
          class="skill-node-tag"
          :style="{ left: skill.x + '%', top: skill.y + '%' }"
          @click="selectSkill(skill)"
        >
          <span
            class="doodle-skill-badge"
            :class="{ active: selectedSkill.name === skill.name }"
          >
            {{ skill.name }}
          </span>
        </div>
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref } from 'vue'

const skillList = ref([
  { name: 'JavaScript', 
    x: 48, 
    y: 25,
    project: {
      title: '撲克牌遊戲-21點',
      desc: '基於JavaScript (ES6) 開發的單機 21 點遊戲。玩家將與莊家進行 1 對 1 對決，體驗籌碼下注、比點數與破產的樂趣！',
      demoUrl:'https://eishinchen.github.io/BlackJack/',
      githubUrl: 'https://github.com/EishinCHEN/BlackJack'
    }
  },
  {
    name: 'Vue',
    x: 28,
    y: 29,
    project: {
      title: 'RPG 風格互動式履歷網站',
      desc: '使用 Vue 3 + Vite 開發的互動式個人履歷。',
      demoUrl: 'https://eishinchen.github.io/Resume/',
      githubUrl: 'https://github.com/EishinCHEN/Resume'
    }
  },
  {
    name: 'Python',
    x: 32,
    y: 40,
    project: {
      title: '台鐵高鐵預售票爬蟲',
      desc: '透過網頁爬蟲擷取高鐵與台鐵官網資訊，結合 LINE Notify 自動化傳送通知，提醒訂閱者購票。',
      githubUrl: 'https://github.com/EishinCHEN/hsr_ticket_notifier'
    }
  },
  { name: 'C#', x: 75, y: 25 },
  { name: 'Web API', x: 22, y: 52 },
  { name: 'Message Queue', x: 60, y: 40 },
  { name: 'Docker', x: 78, y: 48 },
  { name: 'SQL Server', x: 29, y: 71 },
  { name: 'Oracle', x: 70, y: 66 },
  { name: 'BigQuery', x: 50, y: 51 }
])

// 預設選擇第一個有作品的技能
const selectedSkill = ref(skillList.value[0])

const selectSkill = (skill) => {
  selectedSkill.value = skill
}
</script>

<style scoped>
/* 左右橫向分欄容器 */
.skill-split-layout {
  display: flex;
  gap: 16px;
  width: 100%;
  align-items: stretch; /* 兩邊等高 */
}

/* 左半邊作品卡片區 (寬度約 42%) */
.project-panel {
  flex: 0 0 42%;
  background-color: #ffffff;
  border: 2.5px solid #5c2700;
  border-radius: 12px;
  padding: 16px;
  display: flex;
  flex-direction: column;
  justify-content: space-between;
  box-sizing: border-box;
}

.panel-title {
  display: flex;
  justify-content: space-between;
  align-items: center;
  font-weight: bold;
  color: #5c2700;
  font-size: 14px;
  border-bottom: 2px dashed #937157;
  padding-bottom: 8px;
  margin-bottom: 12px;
}

.active-tech-badge {
  font-size: 11px;
  background-color: #937157;
  color: #f7f4f2;
  padding: 2px 8px;
  border-radius: 10px;
}

.project-content {
  flex: 1;
  display: flex;
  flex-direction: column;
}

.project-name {
  margin: 0 0 8px 0;
  font-size: 15px;
  color: #5c2700;
}

.project-desc {
  font-size: 13px;
  color: #5c2700;
  line-height: 1.5;
  margin: 0 0 16px 0;
  flex: 1;
}

.empty-project {
  flex: 1;
  display: flex;
  align-items: center;
  justify-content: center;
  text-align: center;
  font-size: 13px;
  color: #937157;
  padding: 20px;
}

.project-links {
  display: flex;
  gap: 8px;
  margin-top: auto;
}

/* 塗鴉風格按鈕 */
.doodle-btn {
  font-size: 12px;
  font-weight: bold;
  color: #f7f4f2;
  background-color: #5c2700;
  border: 2px solid #5c2700;
  border-radius: 20px 5px 18px 5px;
  padding: 6px 14px;
  text-decoration: none;
  transition: transform 0.15 ease;
  display: inline-block;
}

.doodle-btn.outline {
  background-color: #f7f4f2;
  color: #5c2700;
}

.doodle-btn:hover {
  transform: scale(1.05);
}

/* 右半邊技能樹區域 (寬度約 58%) */
.tree-panel {
  flex: 1;
  position: relative;
}

.skill-board {
  position: relative;
  width: 100%;
  border: 2.5px solid #5c2700;
  border-radius: 12px;
  overflow: hidden;
  background-color: #f7f4f2;
}

.skill-svg-bg {
  width: 100%;
  height: auto;
  display: block;
}

.skill-node-tag {
  position: absolute;
  transform: translate(-50%, -50%);
  z-index: 10;
  cursor: pointer;
}

.doodle-skill-badge {
  font-size: 11px;
  font-weight: bold;
  color: #5c2700;
  background: #f7f4f2;
  border: 2px solid #5c2700;
  border-radius: 255px 15px 225px 15px/15px 225px 15px 255px;
  padding: 3px 7px;
  white-space: nowrap;
  box-shadow: 2px 2px 0px rgba(92, 39, 0, 0.15);
  display: inline-block;
  transition: all 0.2s ease;
}

.doodle-skill-badge:hover,
.doodle-skill-badge.active {
  transform: scale(1.1) rotate(-1deg);
  background-color: #937157;
  color: #f7f4f2;
}

.empty-project {
  flex: 1;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  text-align: center;
  padding: 16px;
  background-color: #fcfbfa;
  border: 2px dashed #d0c3b9;
  border-radius: 8px;
  margin-top: 4px;
}

.empty-img {
  width: 90px;
  height: 90px;
  object-fit: contain;
  margin-bottom: 12px;
  opacity: 0.85;
  filter: drop-shadow(1px 1px 0px rgba(92, 39, 0, 0.15));
}

.empty-text {
  font-size: 13px;
  color: #5c2700;
  margin: 0;
  line-height: 1.5;
}

.empty-subtext {
  font-size: 11px;
  color: #937157;
  display: inline-block;
  margin-top: 4px;
}
</style>