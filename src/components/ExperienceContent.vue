<template>
  <div class="exp-split-layout">
    <!-- 左半邊：工作經歷詳細卡片 (寬度約 45%) -->
    <div class="detail-panel">
      <div class="panel-header">
        <span>職涯足跡</span>
        <span class="active-location-badge">{{ selectedExp.location }}</span>
      </div>

      <div class="exp-info">
        <h3 class="company-name">{{ selectedExp.company }}</h3>
        <div class="job-meta">
          <span class="role">{{ selectedExp.role }}</span>
          <span class="period">{{ selectedExp.period }}</span>
        </div>
        
        <ul class="task-list">
          <li v-for="(task, index) in selectedExp.tasks" :key="index">
            {{ task }}
          </li>
        </ul>
      </div>
    </div>

    <!-- 右半邊：東亞地圖區域 (寬度約 55%) -->
    <div class="map-panel">
      <div class="map-board">
        <img src="@/assets/experience-map.svg" class="map-img" alt="Experience Map" />

        <!-- 依地理位置繪製標籤點位 -->
        <div
          v-for="exp in expList"
          :key="exp.id"
          class="map-marker-node"
          :style="{ left: exp.x + '%', top: exp.y + '%' }"
          @click="selectExp(exp)"
        >
          <div
            class="clean-exp-marker"
            :class="{ active: selectedExp.id === exp.id }"
        >
            <!-- 左側圖標 -->
            <span class="pin-icon">📍</span>
            <!-- 右側公司名稱 -->
            <span class="marker-text">{{ exp.label }}</span>
        </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref } from 'vue'

// 根據圖片的地理位置預設相對百分比 (X%, Y%)
const expList = ref([
  {
    id: 'hiroshima',
    label: '廣島格蘭王子飯店',
    company: '廣島 格蘭王子飯店',
    location: '日本 廣島',
    role: '研修生',
    period: '2018',
    x: 42,
    y: 43,
    tasks: [
      '大廳賓客接待與引導服務',
      '客房整備與房務品質管理',
      '餐廳現場營運與餐飲服務'
    ]
  },
  {
    id: 'tokyo',
    label: '太陽城王子飯店',
    company: '池袋 太陽城王子飯店',
    location: '日本 東京',
    role: '接待人員',
    period: '2019 - 2020',
    x: 62,
    y: 37,
    tasks: [
      '前檯旅客入住手續與諮詢服務',
      '巴士票券銷售、帳務與數量控管',
      '提供中/日/英語多國籍客務接待',
      '處理外籍旅客突發/緊急需求'
    ]
  },
  {
    id: 'kagaya',
    label: '加賀屋',
    company: '加賀屋溫泉酒店',
    location: '台灣 台北',
    role: '櫃檯接待員',
    period: '2020 - 2021',
    x: 35,
    y: 69,
    tasks: [
      '前檯旅客入住手續與諮詢服務',
      '飯店公告之英日文翻譯製作',
      '外籍旅客之日文及英文對應'
    ]
  },
  {
    id: 'kerry',
    label: '嘉里大榮物流',
    company: '嘉里大榮物流',
    location: '台灣 台北',
    role: '程式設計師',
    period: '2022 - 2025',
    x: 35,
    y: 72,
    tasks: [
      '內部系統跨部門需求溝通與追蹤',
      '撰寫單元測試，提高測試覆蓋率',
      'Vue.js 與 Web API 前端組件開發',
      'Message Queue 串連分散式系統 ',
      'Docker 搭配 Jinkins 自動化 DI/CD ',
    ]
  },
  {
    id: 'isnet',
    label: '台灣智慧生活網',
    company: '55688集團-台灣智慧生活網',
    location: '台灣 新北',
    role: '數據工程師',
    period: '2025 - 至今',
    x: 34,
    y: 76,
    tasks: [
      '開發資料血緣追蹤系統',
      '自動化監控 Schema 差異',
      '參與資料庫設計與關聯建構',
      '建構團隊專屬 Python Library'
    ]
  }
])

// 預設選中最近的一份工作
const selectedExp = ref(expList.value[4])

const selectExp = (exp) => {
  selectedExp.value = exp
}
</script>

<style scoped>
/* 橫向雙欄佈局 */
.exp-split-layout {
  display: flex;
  gap: 16px;
  width: 100%;
  align-items: stretch;
}

/* 左半邊詳細資料區 */
.detail-panel {
  flex: 0 0 45%;
  background-color: #ffffff;
  border: 2.5px solid #5c2700;
  border-radius: 12px;
  padding: 16px;
  display: flex;
  flex-direction: column;
  box-sizing: border-box;
}

.panel-header {
  display: flex;
  justify-content: space-between;
  align-items: center;
  font-weight: bold;
  color: #5c2700;
  font-size: 13px;
  border-bottom: 2px dashed #937157;
  padding-bottom: 8px;
  margin-bottom: 12px;
}

.active-location-badge {
  font-size: 11px;
  background-color: #937157;
  color: #f7f4f2;
  padding: 2px 8px;
  border-radius: 10px;
}

.company-name {
  margin: 0 0 6px 0;
  font-size: 16px;
  color: #5c2700;
}

.job-meta {
  display: flex;
  justify-content: space-between;
  font-size: 12px;
  font-weight: bold;
  color: #937157;
  margin-bottom: 12px;
}

.task-list {
  padding-left: 18px;
  margin: 0;
  font-size: 13px;
  color: #5c2700;
  line-height: 1.6;
}

.task-list li {
  margin-bottom: 6px;
}

/* 右半邊地圖區 */
.map-panel {
  flex: 1;
}

.map-board {
  position: relative;
  width: 100%;
  border: 2.5px solid #5c2700;
  border-radius: 12px;
  overflow: hidden;
  background-color: #f7f4f2;
}

.map-img {
  width: 100%;
  height: auto;
  display: block;
}

/* 標籤定位與點擊樣式 */
.map-marker-node {
  position: absolute;
  transform: translate(-12px, -50%);
  z-index: 10;
  cursor: pointer;
}

.clean-exp-marker {
  display: flex;
  align-items: center;
  gap: 4px;
  white-space: nowrap;
  transition: transform 0.2s ease;
}

.marker-text {
  font-size: 12px;
  font-weight: bold;
  color: #5c2700; 
  text-shadow: 
    1px 1px 0 #f7f4f2,
    -1px -1px 0 #f7f4f2,
    1px -1px 0 #f7f4f2,
    -1px 1px 0 #f7f4f2;
  transition: color 0.2s ease;
}

.clean-exp-marker:hover,
.clean-exp-marker.active {
  transform: scale(1.1);
}

.clean-exp-marker:hover .marker-text,
.clean-exp-marker.active .marker-text {
  color: #937157;
}

.pin-icon {
  font-size: 13px;
  line-height: 1;
}
</style>