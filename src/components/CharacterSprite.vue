<template>
  <div 
    class="character"
    :style="{ left: x + 'px', top: y + 'px' }"
  >
    🚶‍♀️
  </div>
</template>

<script setup>
defineProps({
  x: { type: Number, default: 500 },
  y: { type: Number, default: 300 }
})
</script>

<style scoped>
.character {
  position: absolute;
  font-size: 32px;
  transform: translate(-50%, -100%);
  transition: left 0.4s ease-in-out, top 0.4s ease-in-out;
  z-index: 10;
  pointer-events: none;
}
</style>