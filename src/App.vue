<template>
  <div id = "main">
    <splashscreen time = "2000"></splashscreen>
    <about-guru></about-guru>
  </div>
</template>

<script>
import splashscreen from './components/splashscreen.vue';
import AboutGuru from './components/AboutGuru.vue';

export default {
  name: 'App',

  components: {
    splashscreen,
    AboutGuru,
  },

  data: () => ({
    splash: false
  }),
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
