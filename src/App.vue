<template>
  <a-scene>
    <a-assets>
      <!-- Images. -->
      <!-- <img
        id="city"
        src="http://ac-0uhksb6k.clouddn.com/295312cf96a748ce62f5.jpg?imageView2/2/w/4096/h/2048/q/100/format/jpg"
      >-->
      <img
        id="city"
        src="https://dn-0uhksb6K.qbox.me/b193d3b6401aca9c744a.jpg?imageView2/2/w/4096/h/2048/q/100/format/jpg"
      >
    </a-assets>

    <!-- 360-degree image. -->
    <a-sky id="image-360" radius="10" src="#city"></a-sky>
  </a-scene>
</template>

<script>
import firebase from 'firebase';

export default {
  data() {
    return {
      images: []
    }
  },
  created() {
    // Fetcth VR data from firebase
    const liveTourId = "554149"
    const VRCamFirebase = firebase.initializeApp({
      databaseURL: 'https://vr-cam-161603.firebaseio.com',
      serviceAccount: require('../disc/serviceAccountKey.json')
    })
    const fetchPanoramas = VRCamFirebase.database().ref('/panoramas').orderByChild('Building').equalTo(liveTourId)
    fetchPanoramas.once('value', snapshot => {
      let snapshotData = snapshot.val()
      // for (let i in snapshotData) {
      //   this.images.push(snapshotData[i].data.desktopUrl)
      // }
      // console.log(this.images)
      console.log(snapshotData)
    })
  }
}
</script>

<style>
</style>
