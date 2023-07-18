<template>
  <div>
    <svg :style="{ width: width, height: height }">
      <use :xlink:href="prefix+name"></use>
    </svg>
  </div>
</template>

<script setup lang="ts">
defineProps({
  prefix:{
    type:String,
    default:'#icon-'
  },
  name: String,
  //svg图标的颜色
  color: {
    type: String,
    default: ""
  },
  //svg宽度
  width: {
    type: String,
    default: '16px'
  },
  //svg高度
  height: {
    type: String,
    default: '16px'
  }

})
</script>
<style scoped>
</style>
