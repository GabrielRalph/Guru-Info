<template>
  <div id = "main">
    <splashscreen v-model = "load"></splashscreen>
    <about-guru :edit = "edit" v-if = "database.length > 0" v-model = "database"></about-guru>
  </div>
</template>

<script>
import splashscreen from './components/splashscreen.vue';
import AboutGuru from './components/AboutGuru.vue';
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
    edit: false
  }),
  created(){
    firebase.database().ref().on('value', (sc) =>  {
      this.database = sc.val().data
      this.edit = sc.val().edit
      console.log(sc.val());
      setTimeout(()=>{
        this.load = true;
      }, 1000)
    })
  }
};
</script>

<style>
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
  -ms-overflow-style: none;
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
