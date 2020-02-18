<template>
  <div v-if = "shown" id = "splashscreen">
    <img src = "../assets/logoINV.svg" />
  </div>
</template>

<script>
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
    data: () => ({
      theta: 0,
      y: 0,
      x: 0,
      shown: true,

    }),

    watch: {
      value: function(a){
        if(a){
          this.fade();
        }else{
          this.show();
        }
      }
    },
    methods: {
      moveStep(){
        this.theta += 2*Math.PI/(this.frequency*this.fps);
        this.y = Math.sin(this.theta*4)*17;
        this.x = Math.sin(this.theta)*40;
        document.documentElement.style.setProperty('--y', this.y + "px");
        document.documentElement.style.setProperty('--x', this.x + "px");
      },
      iterator(x){
        setTimeout(() => {
          if(this.shown){
            if(x>0){
              this.moveStep();
              this.iterator(x-1);
            }else if(x == -1){
              this.moveStep();
              this.iterator(-1);
            }else if(x == 0){
              this.fade();
              this.iterator(-1);
            }
          }
        }, 1000/this.fps)
      },
      fade(){
        document.documentElement.style.setProperty('--fader', "0");
        if(!this.value) {
          this.$emit('input', true);
        }
        setTimeout(() => {
          this.$emit('faded', true);
          this.shown = false;
        }, this.fadeTime)
      },
      show(){
        this.shown = true;
        document.documentElement.style.setProperty('--fader', "1");
        if(this.time != -1){
          this.iterator(this.time/(1000/this.fps));
        }else{
          this.iterator(-1);
        }
      }
    },
    created(){
      document.documentElement.style.setProperty('--fade-time', this.fadeTime/1000 + "s");
      this.show();
    }

  }
</script>

<style>
:root{
  --y: 0px;
  --x: 0px;
  --fader: 1;
  --fade-time: 0.5s;
}

#splashscreen{

  position: fixed;
  top: 0;
  left: 0;
  height: 100%;
  width: 100%;
  z-index: 1000;
  background:#070706;
  overflow: hidden;
  opacity: var(--fader);
  transition: var(--fade-time) opacity ease-out;
}
#splashscreen img{
  width: 300px;
  position: fixed;

  top: calc(50% - 300px / 2 + var(--y));
  left: calc(50% - 300px / 2 + var(--x));
}
</style>
