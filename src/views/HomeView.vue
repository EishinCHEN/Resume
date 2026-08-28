<template>
  <div class="viewport-wrapper">
    <!-- 地圖主容器：強制維持 16:9 比例，並在螢幕內等比置中縮放 -->
    <div class="map-board">
      <img src="@/assets/map-bg.svg" class="map-svg-bg" alt="Map" />

      <!-- 標籤用 % 定位，固定在 SVG 圖上的相對位置 -->
      <div
        v-for="(node, key) in mapNodes"
        :key="key"
        class="map-node-target"
        :style="{ left: node.x + '%', top: node.y + '%' }"
        @mouseenter="handleNodeHover(key)"
        @mouseleave="handleNodeLeave"
        @click="openNodeModal(key)"
      >
        <div class="doodle-tag">{{ node.name }}</div>
      </div>
    </div>

    <!-- 個人狀態卡、對話框 固定在畫面最外層的 -->
    <StatusCard class="ui-status" />
    <DialogBox :text="currentDialogText" />

    <!-- 視窗 Modal -->
    <DetailModal
      :isOpen="isModalOpen"
      :title="activeNode.name"
      @close="isModalOpen = false"
    >
      <component :is="modalComponent" />
    </DetailModal>
  </div>
</template>

<script setup>
import { ref, shallowRef } from 'vue'
import StatusCard from '@/components/StatusCard.vue'
import DialogBox from '@/components/DialogBox.vue'
import DetailModal from '@/components/DetailModal.vue'
import SkillTreeContent from '@/components/SkillTreeContent.vue'
import ExperienceContent from '@/components/ExperienceContent.vue'
import AboutContent from '@/components/AboutContent.vue'

// 定義節點位置 
// 計算公式：X% = (原px / 1920) * 100 , Y% = (原px / 1080) * 100
const mapNodes = {
  about: { name: '關於我', x: 70, y: 65, hint: '點擊查看關於我的詳細簡介！' },
  skills: { name: '技能樹', x: 44, y: 55, hint: '點擊查看我的專業技能與工具！' },
  experience: { name: '工作經歷', x: 47, y: 35, hint: '點擊查看過往的工作與專案經歷！' }
}
const DEFAULT_DIALOG = '歡迎來到我的網站！請滑鼠移至或點擊地圖上的標籤開始探索吧！'

const isModalOpen = ref(false)
const activeNode = ref({ key: '', name: '' })
const currentDialogText = ref(DEFAULT_DIALOG)
const modalComponent = shallowRef(null)

let timer = null

// 模擬打字機效果
const typeWriter = (text) => {
  clearInterval(timer)
  currentDialogText.value = ''
  let i = 0
  timer = setInterval(() => {
    if (i < text.length) {
      currentDialogText.value += text.charAt(i)
      i++
    } else {
      clearInterval(timer)
    }
  }, 50) // 調整每字印出的毫秒數
}

// 滑鼠移入：即時更新對話框提示
const handleNodeHover = (key) => {
  typeWriter(mapNodes[key].hint)
}

// 滑鼠移出：恢復預設文字
const handleNodeLeave = () => {
  typeWriter(DEFAULT_DIALOG)
}

// 點擊：打開 Modal
const openNodeModal = (key) => {
  const node = mapNodes[key]
  activeNode.value = node

  if (key === 'skills') {
    modalComponent.value = SkillTreeContent
  } else if (key === 'about') {
    modalComponent.value = AboutContent
  } else if (key === 'experience') {
    modalComponent.value = ExperienceContent
  }

  isModalOpen.value = true
}
</script>

<style scoped>
.viewport-wrapper {
  width: 100vw;
  height: 100vh;
  background-color: #f7f4f2;
  display: flex;
  align-items: center;
  justify-content: center;
  position: relative;
  overflow: hidden;
}

.map-board {
  position: relative;
  width: 100vw;
  height: calc(100vw * 9 / 16);
  max-height: 100vh;
  max-width: calc(100vh * 16 / 9);
  aspect-ratio: 16 / 9; /* 鎖定比例 */
}

.map-svg-bg {
  width: 100%;
  height: 100%;
  display: block;
  pointer-events: none;
}


.ui-status {
  position: absolute;
  top: 20px;
  left: 20px;
  z-index: 10;
}



/* 塗鴉風點擊標籤 */
.map-node-target {
  position: absolute;
  transform: translate(-50%, -50%);
  cursor: pointer;
  z-index: 15;
}

.map-node-target:nth-child(1) .doodle-tag { animation-delay: 0s; }
.map-node-target:nth-child(2) .doodle-tag { animation-delay: 0.8s; }
.map-node-target:nth-child(3) .doodle-tag { animation-delay: 1.6s; }

@keyframes tagFloat {
  0%, 100% {
    transform: translateY(0px) rotate(-1deg);
  }
  50% {
    transform: translateY(-6px) rotate(1deg);
  }
}

.doodle-tag {
  font-size: 14px;
  font-weight: bold;
  color: #5c2700;
  background: #f7f4f2;
  border: 2.5px solid #5c2700;
  border-radius: 255px 15px 225px 15px/15px 225px 15px 255px;
  padding: 6px 14px;
  white-space: nowrap;
  animation: tagFloat 3s ease-in-out infinite;
  display: inline-block;
}

.doodle-tag:hover {
  animation-play-state: paused;
  transform: scale(1.15) rotate(-2deg) !important;
  background-color: #937157;
  color: #f7f4f2;
  transition: transform 0.15s ease;
}

.ui-status {
  position: fixed;
  top: 20px;
  left: 20px;
  z-index: 20;
}
</style>