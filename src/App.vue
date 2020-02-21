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
      this.database = sc.val().cms.pages
      this.edit = sc.val().edit
      this.editable = false
      this.cc = sc.val().cc
      this.cc2 = sc.val().cc2
      this.assets = sc.val().assets
      console.log(sc.val());
      setTimeout(()=>{
        this.load = true;
      }, 2000)
    })
  }
};
</script>

<style>
@import url('https://fonts.googleapis.com/css?family=Roboto:300,300i,400,400i,500,500i,700,700i,900,900i&display=swap');
@font-face {
    font-family: 'Guru';
    src: url('./assets/subset-Guru-Regular.eot');
    src: url('./assets/subset-Guru-Regular.eot?#iefix') format('embedded-opentype'),
        url('./assets/subset-Guru-Regular.woff2') format('woff2'),
        url('./assets/subset-Guru-Regular.woff') format('woff'),
        url('./assets/subset-Guru-Regular.svg#Guru-Regular') format('svg');
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
  background: #070706;
  color: #FEF9E4;

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
