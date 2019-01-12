<template>
  <div>aaa</div>
</template>

<script>
import firebase from 'firebase';

export default {
  created() {
    // Fetcth VR data from firebase
    const liveTourId = "554149"
    const VRCamFirebase = firebase.initializeApp({
      databaseURL: 'https://vr-cam-161603.firebaseio.com',
      serviceAccount: require('../disc/serviceAccountKey.json')
    })
    const fetchPanoramas = VRCamFirebase.database().ref('/panoramas').orderByChild('Building').equalTo(liveTourId)
    fetchPanoramas.once('value', snapshot => {
      console.log(snapshot.val())
    })
  }
}
</script>

<style>
</style>
