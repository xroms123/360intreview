<template>
<div class = "scene" v-bind:class = "{'show' : show}">
  <a-scene>
    <a-sky id="image-360" position="0 0 0" radius="10" v-bind:src = "src">
      <a-animation attribute="rotation" dur="8000" from="90 0 0" to="0 0 0"></a-animation>
    </a-sky>
  </a-scene>
</div>
</template>

<script>
export default {
  props: ['src', 'show'],
}
</script>

<style scoped>
.scene {
  opacity: 0;
  transition: opacity 1s ease-in-out;
}
.show {
  opacity: 1;
}
</style>
