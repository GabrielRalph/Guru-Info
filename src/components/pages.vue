<template>
  <div id = "about-guru">
      <div class = "right" @click = "next('right')" v-if = "right_possible">
        <v-icon color = "var(--guru-color)" size = "100px">keyboard_arrow_right</v-icon>
      </div>
      <div  class = "left" @click = "next('left')" v-if = "left_possible">
        <v-icon color = "var(--guru-color)" size = "100px">keyboard_arrow_left</v-icon>
      </div>
      <div class = "bottom">
        <tr style = "width: 50%">
          <td style = "width: 50%"></td>
          <td v-for = "i in value.length" :key = "'lctn_'+i"><div class = "lctn" @click = "pg = i-1"><div :class ="{show: pg+1 == i}"></div></div></td>
          <td style = "width: 50%"></td>
        </tr>
      </div>
      <div class = "top">
        <span>{{cc}}</span>
        <templat v-if = "editable">
          <v-icon color = "var(--guru-color)" size = "50px" @click = "save">save</v-icon>
          <v-icon color = "var(--guru-color)" size = "50px" @click = "addPage()">add</v-icon>
          <v-icon color = "var(--guru-color)" size = "50px" @click = "removePage()">remove</v-icon>
          <v-icon color = "var(--guru-color)" size = "50px" @click = "editToggle">visibility</v-icon>
        </templat>
      </div>

      <v-window v-model = "pg">
        <v-window-item v-for = "(page, i) in value" :key = "'page_'+i">
            <div v-html = "page.content">

            </div>
            <ckeditor  :editor="editor" v-if="edit" :value = "page" @input = "update(i, $event)"></ckeditor>

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

      editable: {
        default: false
      },
      cc: {
        default: "placeholder"
      },
      cc2:{
        default: "copy right GG"
      },
      assets: {

      }
    },
    data: () => ({
      editor: ClassicEditor,
      p1: '',
      pg: 0,
      pgs: 7,
      edit: false,

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
      addAssets(page){
        return page.replace(/<p>%asset(\d)+%<\/p>/gi, (x, y) => {
          return this.assets[y]
        });
      },
      addPage(){
        this.pgs++;
        var tempObject = JSON.parse(JSON.stringify(this.value));
        tempObject.push('<h2>New Page</h2>');
        this.$emit('input', tempObject)
        this.pg = this.pgs - 1;
        this.$forceUpdate()
      },
      removePage(){
        this.pgs--;
        var tempObject = JSON.parse(JSON.stringify(this.value));
        tempObject.splice(this.pg, 1);
        this.$emit('input', tempObject)
        this.$forceUpdate()
      },
      update(i, page){
        var tempObject = JSON.parse(JSON.stringify(this.value));
        tempObject[i] = page;
        this.$emit('input', tempObject)
        this.$forceUpdate()
      },
      save(){
        firebase.database().ref('/pages').set(this.value)
      },
      editToggle(){
        this.edit = !this.edit
      }
    },
    computed: {
      left_possible(){
        return this.pg > 0
      },
      right_possible(){
        return this.pg < this.value.length -1;
      }
    },
    created(){
      window.addEventListener('resize', ()=> {cssSet('--padding', ( ((window.innerWidth - 900)/2 < 100 )?(100):( (window.innerWidth - 900)/2 )) + 'px')});
      cssSet('--padding', ( ((window.innerWidth - 1100)/2 < 100 )?(100):( (window.innerWidth - 1100)/2 )) + 'px')
      this.fade(3500);
      this.pgs = this.value.length
    }


  }
</script>

<style>
:root{
  --fact: 10;
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
  border: 7.5px solid var(--guru-color);
  margin: -7.5px -7.5px;
  width: 30px;
  height: 30px;
  transition: 0.5s;
}
.lctn div:not(.show){
  opacity: 0;
}
.lctn div:hover{
  opacity: 0.3;
}
.show{
  opacity: 0.5;
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
  background: var(--guru-color);
}
#about-guru{
  background: #070706;
  padding:  100px var(--padding);
}
.bottom, .top{
  position: fixed;
  left: 0;
  z-index: 10;
  opacity: var(--opacity);
  transition: 0.7s;
}
.bottom{
  bottom: 0;
}
.top {
  width: 100%;
  top: 0;
  /* padding-left: calc(100% - var(--icon-size) - (var(--padding) - var(--icon-size))/4); */
  padding: calc((var(--padding) - var(--icon-size))/4);
}
.top span{
  float: right;
  padding: 20px;
}
i{
  color: #0798ff;
  font-style: normal;
}
blockquote p{
  font-size: 20px;
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
h2{
  font-size: 70px;
  padding: 20px 0;
  color: var(--guru-color);
}

h4{
  font-size: 30px;
  margin-top: 0;
  color: var(--guru-color)
}
h2 ~ h4{
  color: white;
  display: inline-block;
  line-height: 50px;
  padding: 10px 30px;
  border-radius: 50px;
  background: var(--guru-color);
  border: 4px solid var(--guru-color);
}
p{
  font-size:  25px;
  letter-spacing: 2px;
  font-weight: 400;
  line-height: 40px;
  color: #FEF9E4;
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
  height: calc(11.8px * var(--fact));
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
.phone-in-key{
  width: 200px;
  height: 200px;
  position: relative;
}
.key{
  top:65px;
  position: absolute;
  left: 37px;
}
.phone{
  top:0;
  left:0;
  position: absolute;
}





</style>
