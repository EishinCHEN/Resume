<template>
  <Transition name="doodle-pop">
    <div v-if="isOpen" class="modal-overlay" @click.self="close">
      <div class="doodle-modal">
        <!-- 關閉按鈕 -->
        <button class="close-btn" @click="close">✕</button>

        <!-- 視窗標題 -->
        <div class="modal-header">
          <h2>{{ title }}</h2>
        </div>

        <!-- 視窗動態內容區 -->
        <div class="modal-body">
          <slot></slot>
        </div>
      </div>
    </div>
  </Transition>
</template>

<script setup>
defineProps({
  isOpen: Boolean,
  title: String
})

const emit = defineEmits(['close'])
const close = () => emit('close')
</script>

<style scoped>
/* Vue 過場動畫定義 */
.doodle-pop-enter-active {
  animation: doodleIn 0.35s cubic-bezier(0.175, 0.885, 0.32, 1.275);
}

.doodle-pop-leave-active {
  animation: doodleIn 0.25s reverse linear;
}

/* 漫畫風彈跳幀 */
@keyframes doodleIn {
  0% {
    opacity: 0;
    transform: scale(0.5) rotate(-5deg);
  }
  70% {
    transform: scale(1.03) rotate(1.5deg);
  }
  100% {
    opacity: 1;
    transform: scale(1) rotate(0deg);
  }
}

.modal-overlay {
  position: fixed;
  top: 0;
  left: 0;
  width: 100vw;
  height: 100vh;
  background: rgba(92, 39, 0, 0.25);
  backdrop-filter: blur(2px);
  display: flex;
  align-items: center;
  justify-content: center;
  z-index: 100;
}

.doodle-modal {
  background-color: #f7f4f2;
  border: 4px solid #5c2700;
  border-radius: 20px 225px 20px 255px/225px 20px 255px 20px;
  padding: 30px;
  width: 80%;
  max-width: 820px;
  max-height: 85vh;
  overflow-y: auto;
  position: relative;
  -ms-overflow-style: none; /* IE and Edge */
  scrollbar-width: none; /* Firefox */
}

.doodle-modal::-webkit-scrollbar {
  display: none; /* Chrome / Safari / Opera */
}

.close-btn {
  position: absolute;
  top: 15px;
  right: 20px;
  background: none;
  border: 2px solid #937157;
  border-radius: 50%;
  color: #5c2700;
  font-size: 18px;
  font-weight: bold;
  width: 32px;
  height: 32px;
  cursor: pointer;
  display: flex;
  align-items: center;
  justify-content: center;
  z-index: 10;
}

.close-btn:hover {
  background-color: #937157;
  color: #f7f4f2;
}

.modal-header h2 {
  color: #5c2700;
  border-bottom: 2px stroke #937157;
  padding-bottom: 10px;
  margin-top: 0;
}

.modal-body {
  color: #5c2700;
  line-height: 1.6;
}

@media (max-width: 768px) {
  .doodle-modal {
    width: 90%;
    padding: 20px 16px;
    max-height: 90vh;
  }

  /* 將 Slot 的橫向 Flex 布局改為上下縱向排列 */
  .modal-body :deep([class*='-split-layout']) {
    flex-direction: column !important;
  }

  /* 將子面板寬度重置為 100% 滿版 */
  .modal-body :deep([class*='-panel']),
  .modal-body :deep(.detail-panel),
  .modal-body :deep(.profile-panel) {
    flex: 1 1 100% !important;
    width: 100% !important;
  }
}
</style>