<template>
  <div class="doodle-status-card">
    <!-- 大頭貼區域 -->
    <div class="avatar-box">
      <img src="@/assets/avatar.svg" alt="Avatar" class="avatar-icon" />
    </div>

    <!-- 數值與資訊區 -->
    <div class="info-box">
      <div class="header">
        <span class="level">Lv. {{ age }}</span>
        <span class="name">陳映臻</span>
      </div>

      <!-- EXP 進度條-->
      <div class="bar-group">
        <div class="bar-label">EXP</div>
        <div class="bar-bg">
          <div class="bar-fill exp" :style="{ width: expProgress + '%' }"></div>
        </div>
        <span class="bar-text">{{ expProgress }}%</span>
      </div>

      <!-- HP 進度條-->
      <div class="bar-group">
        <div class="bar-label">HP</div>
        <div class="bar-bg">
          <div class="bar-fill hp" :style="{ width: (hp.current / hp.max) * 100 + '%' }"></div>
        </div>
        <span class="bar-text">{{ hp.current }}/{{ hp.max }}</span>
      </div>

      <!-- MP 進度條 (代表技能/專案解題能量) -->
      <div class="bar-group">
        <div class="bar-label">MP</div>
        <div class="bar-bg">
          <div class="bar-fill mp" :style="{ width: (mp.current / mp.max) * 100 + '%' }"></div>
        </div>
        <span class="bar-text">{{ mp.current }}/{{ mp.max }}</span>
      </div>
    </div>
  </div>
</template>

<script setup>
import { computed, ref } from 'vue'

const birthDate = new Date(1997, 1, 1)

// 自動計算年齡 (等同於 Lv)
const age = computed(() => {
  const today = new Date()
  let calcAge = today.getFullYear() - birthDate.getFullYear()
  const monthDiff = today.getMonth() - birthDate.getMonth()
  
  // 如果今年生日還沒到，年齡 - 1
  if (monthDiff < 0 || (monthDiff === 0 && today.getDate() < birthDate.getDate())) {
    calcAge--
  }
  return calcAge
})

// 計算今年過了多少 % 當作今年度的 EXP 經驗值
const expProgress = computed(() => {
  const now = new Date()
  const startOfYear = new Date(now.getFullYear(), 0, 1)
  const endOfYear = new Date(now.getFullYear() + 1, 0, 1)
  const progress = ((now - startOfYear) / (endOfYear - startOfYear)) * 100
  return Math.floor(progress)
})

// 2. HP 與 MP 數值
const hp = ref({ current: 100, max: 100 }) 
const mp = ref({ current: 80, max: 100 })
</script>

<style scoped>
.doodle-status-card {
  display: flex;
  gap: 12px;
  background-color: #f7f4f2;
  border: 3.5px solid #5c2700;
  border-radius: 225px 15px 255px 15px/15px 225px 15px 255px;
  padding: 12px 16px;
  width: 250px;
  box-sizing: border-box;
  animation: handDrawnWobble 4s infinite alternate ease-in-out;
}

.avatar-icon {
  width: 100%;
  height: 100%;
  object-fit: cover;
  transform: scale(1.1);
}

.avatar-box {
  width: 48px;
  height: 48px;
  border: 2.5px solid #937157;
  border-radius: 60% 40% 70% 30% / 40% 50% 60% 50%;
  display: flex;
  align-items: center;
  justify-content: center;
  font-size: 26px;
  background-color: #f7f4f2;
  flex-shrink: 0;
  overflow: hidden;
  padding: 0;
}

.info-box {
  flex: 1;
  font-size: 12px;
  color: #5c2700;
}

.header {
  font-weight: bold;
  font-size: 14px;
  margin-bottom: 6px;
  display: flex;
  gap: 8px;
  align-items: center;
}

.level {
  color: #937157;
}

.bar-group {
  display: flex;
  align-items: center;
  gap: 6px;
  margin-bottom: 4px;
}

.bar-label {
  width: 42px;
  font-weight: bold;
  font-size: 11px;
}

.bar-bg {
  flex: 1;
  height: 9px;
  border: 2px solid #937157;
  border-radius: 10px 4px 8px 5px;
  background: #ffffff;
  overflow: hidden;
  padding: 1px;
}

.bar-fill {
  height: 100%;
  border-radius: 2px;
  transition: width 0.3s ease;
}

.bar-fill.exp {
  background-color: #937157;
}

.bar-fill.hp {
  background-color: #5c2700;
}

.bar-fill.mp {
  background-color: #c4a482;
}

.bar-text {
  font-size: 10px;
  font-weight: bold;
  width: 45px;
  text-align: right;
}


@keyframes handDrawnWobble {
  0% {
    border-radius: 225px 15px 255px 15px/15px 225px 15px 255px;
  }
  33% {
    border-radius: 20px 255px 15px 225px/225px 15px 255px 20px;
  }
  66% {
    border-radius: 255px 20px 225px 15px/15px 225px 20px 255px;
  }
  100% {
    border-radius: 15px 225px 20px 255px/255px 15px 225px 20px;
  }
}
</style>