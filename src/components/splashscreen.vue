<template>
  <div v-if = "shown" id = "splashscreen">
    <img :src = "weather[code]" />
  </div>
</template>

<script>
var weather = require('weather.js');

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
      code: 'cloudy',
      weather:{
        "clear-day":"https://firebasestorage.googleapis.com/v0/b/guru-admin.appspot.com/o/assets%2Fweather%20icons%2Fguru-weather_1.svg?alt=media&token=eaea8bdf-cab8-4a1d-af22-eeaa4e757e1f",
        "clear-night": "https://firebasestorage.googleapis.com/v0/b/guru-admin.appspot.com/o/assets%2Fweather%20icons%2Fguru-weather_3.svg?alt=media&token=feed4b32-c53a-40c9-a9a3-ea6c4cfed5dd",
        "partly-cloudy-day": "https://firebasestorage.googleapis.com/v0/b/guru-admin.appspot.com/o/assets%2Fweather%20icons%2Fguru-weather_3.svg?alt=media&token=feed4b32-c53a-40c9-a9a3-ea6c4cfed5dd",
        "partly-cloudy-night":"https://firebasestorage.googleapis.com/v0/b/guru-admin.appspot.com/o/assets%2Fweather%20icons%2Fguru-weather_1.svg?alt=media&token=eaea8bdf-cab8-4a1d-af22-eeaa4e757e1f",
        "cloudy": "https://firebasestorage.googleapis.com/v0/b/guru-admin.appspot.com/o/assets%2Fweather%20icons%2Fguru-weather_3.svg?alt=media&token=feed4b32-c53a-40c9-a9a3-ea6c4cfed5dd",
        "rain":"https://firebasestorage.googleapis.com/v0/b/guru-admin.appspot.com/o/assets%2Fweather%20icons%2Fguru-weather_0.svg?alt=media&token=d6e007ec-44b6-40f7-9125-41fc33321e6d",
        "sleet":"https://firebasestorage.googleapis.com/v0/b/guru-admin.appspot.com/o/assets%2Fweather%20icons%2Fguru-weather_4.svg?alt=media&token=744e8707-62b4-478c-9312-9d1339c1e921",
        "snow":"https://firebasestorage.googleapis.com/v0/b/guru-admin.appspot.com/o/assets%2Fweather%20icons%2Fguru-weather_4.svg?alt=media&token=744e8707-62b4-478c-9312-9d1339c1e921",
        "wind": "https://firebasestorage.googleapis.com/v0/b/guru-admin.appspot.com/o/assets%2Fweather%20icons%2Fguru-weather_5.svg?alt=media&token=0274e1a8-4fd8-4bae-9c74-da226b642898",
        "fog": "https://firebasestorage.googleapis.com/v0/b/guru-admin.appspot.com/o/assets%2Fweather%20icons%2Fguru-weather_2.svg?alt=media&token=3316ca2f-038d-4df8-983a-afc570dc881f",
      }


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
      fetch("https://api.darksky.net/forecast/fa5a2c2c8217557d4b1cdde9a875af92/-33.890971, 151.188661").then((response, err) => {
        if (err) throw err
        return response.json()
      }).then((responseJson) => {
        console.log(responseJson)
        this.code = responseJson.current.icon;
      })

      weather.getCurrent("Kansas City", function(current) {
        console.log(current);
      });
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
