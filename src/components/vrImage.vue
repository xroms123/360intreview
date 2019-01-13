<template>
  <a-scene>
    <!-- 360-degree image. -->
    <a-sky id="image-360" radius="10" v-bind:src = "src">
    </a-sky>
  </a-scene>

  
</template>

<script>

export default {
  props: ['src'],
}
</script>

<style scoped>
</style>
