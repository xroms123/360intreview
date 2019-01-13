<template>
<div>
  <VRImage v-bind:src = "onsceneImage"/>
  <div class = "menu">aaa</div>
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
      onsceneImage: ""
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
      console.log(snapshotData)
    })
  }
}
</script>

<style scoped>
.menu {
  width: 100%;
  height: 100px;
  position: fixed;
  bottom: 0;
  background-color: navajowhite;
}
</style>
