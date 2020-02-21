<template>
  <div>

    <div v-if = "shown" id = "splashscreen">

    </div>
    <logo :size = "size" :pos = "pos" :mode = "logomode"></logo>
  </div>

</template>

<script>
import logo from './logo.vue';
  export default {
    name: 'splashscreen',
    props: {
      time: {
        default: -1,
        type: Number,
      },
      fps: {
        default: 40,
        type: Number,
      },
      frequency: {
        default: 4,
        type: Number,
      },
      value: {
        default: false,
        type: Boolean
      },
      fadeTime: {
        default: 500,
        type: Number
      }
    },
    components: {
      logo
    },
    data: () => ({


      pos: '50 50',
      logomode: 'wavey-logo',
      size: '300px',
      shown: true,
    }),
    watch: {
      value: function(a){
        if(a){
          this.pos = '100 0';
          this.size = '120px';
          document.getElementById("splashscreen").style.setProperty('--fader', 0);
          setTimeout(() => {
            this.logomode = 'weather'
            this.shown = false;
          }, 1750);
        }
      }
    },
  }

</script>

<style>


#splashscreen{
  --fader: 1;
  --fade-time: 1s;
  position: fixed;
  top: 0;
  left: 0;
  height: 100%;
  width: 100%;
  z-index: 20;
  background:#070706;
  overflow: hidden;
  opacity: var(--fader);
  transition: var(--fade-time) opacity ease-out;
}


</style>
