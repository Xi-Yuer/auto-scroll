<script setup>
import AutoScroll from './components/auto-scroll.vue'
</script>

<template>
  <div>
    <AutoScroll>
      <h3 v-for="i in 10">{{ i }}</h3>
    </AutoScroll>
  </div>
</template>

<style scoped lang="less"></style>
