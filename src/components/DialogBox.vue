<template>
  <div class="doodle-dialog">
    <div class="avatar-container">
      <img src="@/assets/avatar.svg" alt="Avatar" class="avatar-frame" />
    </div>
    <div class="content">
      <p>{{ text }}</p>
    </div>
  </div>
</template>

<script setup>
defineProps({
  text: {
    type: String,
    default: '歡迎來到我的網站！點擊地圖上的區域開始探索吧！'
  }
})
</script>

<style scoped>
.doodle-dialog {
  position: fixed;
  bottom: 24px;
  left: 50%;
  transform: translateX(-50%);
  z-index: 50;

  display: flex;
  align-items: center;
  gap: 16px;
  background-color: #f7f4f2;
  
  border: 3.5px solid #5c2700;
  border-radius: 255px 15px 225px 15px/15px 225px 15px 255px;
  
  padding: 14px 22px;
  width: min(90vw, 420px);
  box-sizing: border-box;
}

.avatar-container {
  flex-shrink: 0;
}

.avatar-frame {
  font-size: 28px;
  width: 46px;
  height: 46px;
  display: flex;
  align-items: center;
  justify-content: center;
  background-color: #f7f4f2;
  
  border: 2.5px solid #937157;
  border-radius: 60% 40% 70% 30% / 40% 50% 60% 50%;
}

.content p {
  font-size: 15px;
  color: #5c2700;
  font-weight: 700;
  line-height: 1.5;
  margin: 0;
  letter-spacing: 0.5px;
}
</style>