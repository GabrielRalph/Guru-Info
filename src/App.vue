<template>
  <div id = "main">
    <splashscreen v-model = "load"></splashscreen>
    <about-guru :assets = "assets" :cc = "cc" :cc2 = "cc2" :editable = "editable" v-if = "database.length > 0" v-model = "database"></about-guru>
  </div>
</template>
<script>
import splashscreen from './components/splashscreen.vue';
import AboutGuru from './components/pages.vue';
import firebase from 'firebase';
// Your web app's Firebase configuration
  var firebaseConfig = {
    apiKey: "AIzaSyDe5Z5STt003BGd5k3EuGSTu7hWKqZltI4",
    authDomain: "guru-admin.firebaseapp.com",
    databaseURL: "https://guru-admin.firebaseio.com",
    projectId: "guru-admin",
    storageBucket: "guru-admin.appspot.com",
    messagingSenderId: "618229197693",
    appId: "1:618229197693:web:08bdb2afd1457f6f22ba14"
  };
  // Initialize Firebase
  firebase.initializeApp(firebaseConfig);

export default {
  name: 'App',

  components: {
    splashscreen,
    AboutGuru,
  },

  data: () => ({
    splash: false,
    load: false,
    database: [],
    edit: false,
    editable: false,
    cc: 'okay',
    cc2: 'copy right',
    assets: ''
  }),
  created(){
    firebase.database().ref().on('value', (sc) =>  {
      this.database = sc.val().pages
      this.edit = sc.val().edit
      this.editable = sc.val().editable
      this.cc = sc.val().cc
      this.cc2 = sc.val().cc2
      this.assets = sc.val().assets
      console.log(sc.val());
      setTimeout(()=>{
        this.load = true;
      }, 1000)
    })
  }
};
</script>

<style>
@import url('https://fonts.googleapis.com/css?family=Roboto:300,300i,400,400i,500,500i,700,700i,900,900i&display=swap');
@font-face {
    font-family: 'Guru';
    src: url('https://firebasestorage.googleapis.com/v0/b/guru-admin.appspot.com/o/font%2Fsubset-Guru-Regular.eot?alt=media&token=9ada7211-0284-47bc-8174-15ec02a30cb2');
    src: url('https://firebasestorage.googleapis.com/v0/b/guru-admin.appspot.com/o/font%2Fsubset-Guru-Regular.eot?alt=media&token=9ada7211-0284-47bc-8174-15ec02a30cb2?#iefix') format('embedded-opentype'),
        url('https://firebasestorage.googleapis.com/v0/b/guru-admin.appspot.com/o/font%2Fsubset-Guru-Regular.woff2?alt=media&token=53498308-ef9b-40a0-a941-6aa68b568302') format('woff2'),
        url('https://firebasestorage.googleapis.com/v0/b/guru-admin.appspot.com/o/font%2Fsubset-Guru-Regular.woff?alt=media&token=14399fce-6cfd-4e14-aab2-f741f0fa1689') format('woff'),
        url('https://firebasestorage.googleapis.com/v0/b/guru-admin.appspot.com/o/font%2Fsubset-Guru-Regular.svg?alt=media&token=39d31647-16c2-4eba-84ed-386eeba58e24#Guru-Regular') format('svg');
    font-weight: normal;
    font-style: normal;
}
:root{
  --guru-color: #ff9b34;
}
#main{
  margin: 0;
  width: 100%;
  height: 100%;
  overflow: hidden;
}
/* Hide scrollbar for Chrome, Safari and Opera */
body::-webkit-scrollbar {
  display: none;
}

/* Hide scrollbar for IE and Edge */
body {
  font-family: 'Guru', sans-serif;
  -ms-overflow-style: none;
  word-spacing: 25px;

}
.btn{
  position: fixed;
  top: 0;
  left: 0;
  width: 100px;
  height: 100px;
  background: blue;
  z-index: 1000;
}

</style>
