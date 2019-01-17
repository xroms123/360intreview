<template>
<div>
  <VRImage v-bind:src = "onsceneImage" v-bind:show = "isShow"/>

  <!-- Carousel -->
  <div class = "menu">
    <div class = "arrow" v-on:click = "leftClick"> < </div>
      <div class = "menu-carousel">
        <div class = "carousel-bar" ref = "carouselbar" 
             v-bind:style = "{ transform: 'translateX(' +position+ 'px)' }">
          <div class = "menu-item" 
              v-for = "item in images"
              v-on:click = "vrClick(item.url)">
            <img v-bind:src = "item.thumbnail">
            {{item.category}}
          </div>
        </div>
      </div>
    <div class = "arrow" v-on:click = "rightClick"> > </div>
  </div>
</div>

  
</template>

<script>
import firebase from 'firebase';
import VRImage from './components/vrImage.vue';
export default {
  components: {
    'VRImage': VRImage
  },
  data() {
    return {
      liveTourId: 'c951a5af-603f-4003-9d1c-707657febe95',
      images: [],
      onsceneImage: "",
      position: 0,
      carouselWidth: "0",
      isShow: false
    }
  },
  created() {
    // Fetcth VR data from firebase
    const VRCamFirebase = firebase.initializeApp({
      databaseURL: 'https://vr-cam-161603.firebaseio.com',
      serviceAccount: require('../disc/serviceAccountKey.json')
    })

    const fetchPanoramas = VRCamFirebase.database().ref('/panoramas').orderByChild('Building').equalTo(this.liveTourId)
    fetchPanoramas.once('value', snapshot => {
      let snapshotData = snapshot.val()
      for (let i in snapshotData) {
        this.images.push({
          category: snapshotData[i].data.category,
          url: snapshotData[i].data.desktopUrl,
          thumbnail: snapshotData[i].data.thumbnail
        })
      }
      this.onsceneImage = this.images[0].url
      setTimeout(() => {
        this.carouselWidth = this.$refs.carouselbar.clientWidth
      }, 100)
    })
    this.isShow = true;

  },
  methods: {
    vrClick: function (url) {
      this.isShow = false;
      setTimeout(() => {
        this.onsceneImage = url;
        setTimeout(() => {
          this.isShow = true;
        }, 1500);
      }, 1000)
    },
    leftClick: function () {
      let nextPosition = this.position + 175;
      if (nextPosition <= 0) {
        this.position = nextPosition
      }
    },
    rightClick: function () {
      let nextPosition = this.position - 175;
      if (nextPosition > -(this.carouselWidth)) {
        this.position = nextPosition;
      }
    }
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
