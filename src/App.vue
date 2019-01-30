<template>
<div>
  <VRImage v-bind:src = "onsceneImage" v-bind:show = "isShow"/>
</div>

  
</template>

<script>
import firebase from 'firebase';
import VRImage from './components/vrImage.vue';
import Fuji from './fuji.jpg';

export default {
  components: {
    'VRImage': VRImage
  },
  data() {
    return {
      onsceneImage: Fuji,
      isShow: false
    }
  },
  created() {
    this.isShow = true;

  },
  methods: {

  }
}
</script>

<style scoped>
.menu {
  width: 100%;
  height: 150px;
  position: fixed;
  bottom: 0;
  display: inline-flex;
  align-items: center;
  justify-content: center;
  background-color: rgba(182, 182, 182, 0.3);
}
.menu-carousel {
  width: 95%;
  height: 140px;
  overflow: hidden;
}
.carousel-bar {
  height: 140px;
  display: inline-flex;
  align-items: center;
  transition: transform 1s ease;
  color: white;
}
.menu-item {
  width: 160px;
  height: 100px;
  margin: 0 10px;
  cursor: pointer;
}
.menu-item img {
  max-width: 100%;
}
.arrow {
  cursor: pointer;
  margin: 10px;
}
</style>
