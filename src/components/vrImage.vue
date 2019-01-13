<template>
  <a-scene>
    <a-assets>
      <!-- Images. -->
      <!-- <img id="city" src="https://vrcam-prod-cdn.istaging.com/d8b4ba5f-cec1-433b-9ff7-df34fcdb64d5/images/fromImageIO/A0/9_y_4_E_i_e_l_m_A0.jpeg"> -->
    </a-assets>

    <!-- 360-degree image. -->
    <a-sky id="image-360" radius="10" v-bind:src="src"></a-sky>
  </a-scene>

  
</template>

<script>

export default {
  props: ['src']
}
</script>

<style scoped>
</style>
