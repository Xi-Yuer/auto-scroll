<script setup>
import { onDeactivated, onMounted, onUnmounted, ref } from 'vue'

const movebox = ref(null)
const top = ref(0)
const timer = ref(null)

const props = defineProps({
  height: {
    type: String,
    default: '300px',
  },
  speed: {
    type: Number,
    default: 20,
  },
})

onMounted(() => {
  moveFn()
})

const moveFn = () => {
  timer.value = setInterval(() => {
    if (top.value >= movebox.value.offsetHeight / 2) {
      top.value = 0
    }
    top.value++
    movebox.value.style = `transform:translateY(-${top.value}px)`
  }, props.speed)
}

const handleMouseEnter = () => clearTimer()

const clearTimer = () => {
  if (timer.value) {
    clearInterval(timer.value)
  }
}
const handleMouseLeave = () => {
  clearTimer()
  moveFn()
}

onUnmounted(() => clearTimer())
onDeactivated(() => clearTimer())
</script>

<template>
  <div class="outer">
    <div
      ref="movebox"
      @mouseover="handleMouseEnter"
      @mouseleave="handleMouseLeave"
    >
      <slot />
      <slot />
    </div>
  </div>
</template>

<style scoped>
.outer {
  width: 100%;
  height: v-bind(props.height);
  overflow-y: auto;
  position: relative;
  background-color: aqua;
}
::-webkit-scrollbar {
  display: none;
}
</style>
