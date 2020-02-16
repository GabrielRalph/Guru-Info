<template>
  <div id = "about-guru">
      <div class = "right" @click = "next('right')" v-if = "right_possible">
        <v-icon color = "rgb(240, 162, 81)" size = "100px">keyboard_arrow_right</v-icon>
      </div>
      <div  class = "left" @click = "next('left')" v-if = "left_possible">
        <v-icon color = "rgb(240, 162, 81)" size = "100px">keyboard_arrow_left</v-icon>
      </div>
      <div class = "bottom">
        <tr style = "width: 50%">
          <td style = "width: 50%"></td>
          <td v-for = "i in pgs" :key = "'lctn_'+i"><div class = "lctn" @click = "pg = i-1"><div :class ="{show: pg+1 == i}"></div></div></td>
          <td style = "width: 50%"></td>
        </tr>
      </div>
      <div class = "top">
        <span>{{cc}}</span>
        <v-icon v-if = "editable" color = "rgb(240, 162, 81)" size = "100px" @click = "save" @dblclick = "editToggle">save</v-icon>
      </div>

      <v-window v-model = "pg">
        <v-window-item>
            <div v-html = "getelement(0,0)"></div>
            <v-text-field v-if="edit" :value = "value[0][0].text" @input = "setelement(0,0, $event)" height = "50px"></v-text-field>
            <div v-html = "getelement(0,1)"></div>
            <ckeditor  :editor="editor" v-if="edit" :value = "value[0][1].text" @input = "setelement(0,1, $event)"></ckeditor>

        </v-window-item>
        <v-window-item>
          <div class = "sc-phone">
            <div>
              <img src = "../assets/front.svg"/>
            </div>
            <div>
              <img src = "../assets/back.svg"/>
            </div>
          </div>
          <div v-html = "getelement(1,0)"></div>
          <v-text-field v-if="edit" :value = "value[1][0].text" @input = "setelement(1,0, $event)" height = "50px"></v-text-field>
          <div v-html = "getelement(1,1)"></div>
          <ckeditor  :editor="editor"  v-if="edit" :value = "value[1][1].text" @input = "setelement(1,1, $event)"></ckeditor>
          <div v-html = "getelement(1,2)"></div>
          <v-text-field v-if="edit" :value = "value[1][2].text" @input = "setelement(1,2, $event)" height = "50px"></v-text-field>
          <div v-html = "getelement(1,3)"></div>
          <ckeditor  :editor="editor"  v-if="edit" :value = "value[1][3].text" @input = "setelement(1,3, $event)"></ckeditor>
          <div v-html = "getelement(1,4)"></div>
          <v-text-field v-if="edit" :value = "value[1][4].text" @input = "setelement(1,4, $event)" height = "50px"></v-text-field>
          <v-img style = "float: left; margin-right: 20px" src = "..\assets\guru.stucco.org.au_(iPad).png" width = "50%"></v-img>
          <div v-html = "getelement(1,5)"></div>
          <ckeditor  :editor="editor"  v-if="edit" :value = "value[1][5].text" @input = "setelement(1,5, $event)"></ckeditor>

        </v-window-item>

        <v-window-item>
          <div v-html = "getelement(2,0)"></div>
          <v-text-field v-if="edit" :value = "value[2][0].text" @input = "setelement(2,0, $event)" height = "50px"></v-text-field>
          <v-img style = "float: left; margin-right: 20px" src = "..\assets\login.png" width = "30%"></v-img>
          <div v-html = "getelement(2,1)"></div>
          <ckeditor  :editor="editor"  v-if="edit" :value = "value[2][1].text" @input = "setelement(2,1, $event)"></ckeditor>



        </v-window-item>
        <v-window-item>
          <div v-html = "getelement(3,0)"></div>
          <v-text-field v-if="edit" :value = "value[3][0].text" @input = "setelement(3,0, $event)" height = "50px"></v-text-field>
          <div v-html = "getelement(3,1)"></div>
          <ckeditor  :editor="editor"  v-if="edit" :value = "value[3][1].text" @input = "setelement(3,1, $event)"></ckeditor>
        </v-window-item>
        <v-window-item>
          <div v-html = "getelement(4,0)"></div>
          <v-text-field v-if="edit" :value = "value[4][0].text" @input = "setelement(4,0, $event)" height = "50px"></v-text-field>
          <div v-html = "getelement(4,1)"></div>
          <ckeditor  :editor="editor" v-if="edit" :value = "value[4][1].text" @input = "setelement(4,1, $event)"></ckeditor>
        </v-window-item>
        <v-window-item>
          <div v-html = "getelement(5,0)"></div>
          <v-text-field v-if="edit" :value = "value[5][0].text" @input = "setelement(5,0, $event)" height = "50px"></v-text-field>
          <div v-html = "getelement(5,1)"></div>
          <ckeditor  :editor="editor" v-if="edit" :value = "value[5][1].text" @input = "setelement(5,1, $event)"></ckeditor>
        </v-window-item>
        <v-window-item>
          <div v-html = "getelement(6,0)"></div>
          <v-text-field v-if="edit" :value = "value[6][0].text" @input = "setelement(6,0, $event)" height = "50px"></v-text-field>
          <div v-html = "getelement(6,1)"></div>
          <ckeditor  :editor="editor" v-if="edit" :value = "value[6][1].text" @input = "setelement(6,1, $event)"></ckeditor>
        </v-window-item>
        <div class = "copyright">{{cc2}}</div>

      </v-window>
  </div>
</template>

<script>
import firebase from 'firebase'
import ClassicEditor from '@ckeditor/ckeditor5-build-classic';
import 'material-design-icons-iconfont/dist/material-design-icons.css'
let cssSet = (variable, set) => {document.documentElement.style.setProperty(variable, set);}
  export default {
    props: {
      value: {
        required: true
      },
      edit: {
        default: false
      },
      editable: {
        default: false
      },
      cc: {
        default: "placeholder"
      },
      cc2:{
        default: "copy right GG"
      }
    },
    data: () => ({
      editor: ClassicEditor,
      p1: '',
      pg: 0,
      pgs: 7


    }),
    methods: {
      next(direction){
        if(direction == 'left'){
          this.pg --;
        }else if(direction == 'right'){
          this.pg ++;
        }
        this.fade(1000)
      },
      fade(x){
        cssSet('--opacity', 1)
        setTimeout(()=>{
          cssSet('--opacity', 0);
        },x)
      },
      getelement(page, elem){
        console.log(this.value[page][elem])
        if(this.value){
          if(this.value[page]){
            if(this.value[page][elem]){
              return '<'+this.value[page][elem].type+'>'+this.value[page][elem].text+'</'+this.value[page][elem].type+'>'
            }else{
              var tempObject = JSON.parse(JSON.stringify(this.value))
              tempObject[page][elem].text = 'placeHolde'
              tempObject[page][elem].type = 'h1'
              this.$emit('input', tempObject)
            }
          }
        }
      },
      setelement(page, elem, e){
        var tempObject = JSON.parse(JSON.stringify(this.value))
        tempObject[page][elem].text = e
        this.$emit('input', tempObject)
        this.$forceUpdate()
      },
      save(){
        firebase.database().ref('/data').set(this.value)
      },
      editToggle(){
        firebase.database().ref('/edit').set(!this.edit)
      }
    },
    computed: {
      left_possible(){
        return this.pg > 0
      },
      right_possible(){
        return this.pg < this.pgs -1;
      }
    },
    created(){
      window.addEventListener('resize', ()=> {cssSet('--padding', ( ((window.innerWidth - 900)/2 < 100 )?(100):( (window.innerWidth - 900)/2 )) + 'px')});
      cssSet('--padding', ( ((window.innerWidth - 900)/2 < 100 )?(100):( (window.innerWidth - 900)/2 )) + 'px')
      this.fade(3500);
    }


  }
</script>

<style>
@import url('https://fonts.googleapis.com/css?family=Roboto:300,300i,400,400i,500,500i,700,700i,900,900i&display=swap');
:root{
  --fact: 9;
  --padding: 150px;
  --icon-size: 100px;
  --opacity: 1;
}
input{
  font-size: 50px;
}
.lctn div{
  border-radius: 30px;
  position: absolute;
  top: 0;
  left: 0;
  border: 7.5px solid rgba(240, 162, 81, 0.5);
  margin: -7.5px -7.5px;
  width: 30px;
  height: 30px;
  transition: 0.5s;
}
.lctn div:not(.show){
  opacity: 0;
}
.show{
  opacity: 1;
}
.copyright{
  width:100%;
  text-align: center;
  margin-top: 100px;
}
.lctn {
  position: relative;
  margin: 30px;
  width:15px;
  height:15px;
  padding: 7.5px;
  border-radius: 26px;
  background: rgb(240, 162, 81);
}
#about-guru{
  background: white;
  padding:  100px var(--padding);
  font-family: 'Roboto', sans-serif;
}
.bottom, .top{
  position: fixed;
  left: 0;
  z-index: 900;
  opacity: var(--opacity);
  transition: 0.7s;
}
.bottom{
  bottom: 0;
}
.top {
  top: 0;
  padding-left: calc(100% - var(--icon-size) - (var(--padding) - var(--icon-size))/4);
  padding-top: calc((var(--padding) - var(--icon-size))/4);
}
.bottom:hover, .top:hover, .left:hover, .right:hover{
  opacity: 1;
}

.left, .right{
  transition: 0.3s opacity ease-in;
  opacity: var(--opacity);
  position: fixed;
  top: 0;
  padding: calc(50vh - var(--icon-size)/2) calc((var(--padding) - var(--icon-size))/2);
}
.left{
  left: 0;
}
.right{
  right: 0;

}

.h{
  margin-bottom: 100px;
}
.myimg{
  width: 50%;
  float: left;
  margin: 0 20px 20px 0;
}
h1{
  font-size: 70px;
  margin-bottom: 30px;
}
p{
  font-size: 25px;
  font-weight: 400;
}
.txt{
  font-size: 50px;
  font-family: 'Roboto', sans-serif;
  font-weight: 400;
}
/* width */
::-webkit-scrollbar {
  width: 10px;
  border-radius: 5px;
}

/* Track */
::-webkit-scrollbar-track {
  background: rgba(0,0,0,0.1);
}

/* Handle */
::-webkit-scrollbar-thumb {
  background: rgba(0,0,0,0.5);
}

/* Handle on hover */
::-webkit-scrollbar-thumb:hover {
  background: rgba(0,0,0,0.8);
}
.sc-phone{
  width: calc(28px * var(--fact));
  background-image: url('../assets/guru.stucco.org.au_(iPhone 6_7_8).png');
  background-size: 100%;
  height: calc(57.6px  * var(--fact));
  float: right;
  margin:  65px 0 20px 20px ;
  position: relative;
}
.sc-phone div{
  height: calc(12.4px * var(--fact));
  position: absolute;
  top: calc(9.12px * var(--fact));
  left: calc(4.24px * var(--fact));
  perspective: 1000px;
}
.sc-phone div:last-of-type{
  left: calc(12.8px * var(--fact));
}
.sc-phone div img{
  height: 100%;
  transform-origin: left;
  transition: 0.5s transform;
}
.sc-phone div img:hover{
  height: 100%;
  transform: rotateY(-45deg);
}
</style>
