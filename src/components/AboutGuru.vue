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

      <v-window v-model = "pg">
        <v-window-item>
            <h1>Backstory</h1>
            <p>
              As a resident of the Sydney University Student Cooperative (Stucco), I would often lose my key, a small NFC chip. I was not the only one that did this, many fellow residents would also misplace their key or simply forget to bring it on short trips. As a self-taught web developer and student of engineering mechatronics, I decided to develop a solution to the problem at hand. I was able to develop a single page web application that could allow residents to unlock the doors. The implementation of Guru was approved, provided that security protocols where put in place. Guru was a great success with all residents joining the user database and half choosing Guru over the physical key. As Guru became a bookmark or forever open tab on most people's phones, as well as a database with profiles for each resident, I began to develop other functions to aid in general admin and solve problems other residents and committees where having. For instance, before Guru Minute's residents would write minutes in any form of a text editor and then send the minutes to a google group. They would then have to find the link to a google form and tick all residents and applicants who attended the meeting. This tortuous process often led to attendance being overlooked and irregular formatting of minutes.
            </p>
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
          <h1>What is Guru</h1>
          <p>
            Guru is a web application to help residents of student housing with general admin organization and opening doors. Guru has been designed to work in two main modes. Guru will automatically choose the mode based on the users device and screen aspect ratio.
            <br /><br />
          </p>
          <h2>Dashboard</h2>
          <p>
            The mobile dashboard was designed specifically for mobile phones and can be added to the home screen on most mobile handsets.  The mobile dashboard allows users to unlock a given door by tapping on its icon. This will unlock the door for 4 seconds before locking again. Users can also view relevant information such as their rent balance, dates of meetings and attendance respectively.
            <br /><br />
          </p>
          <div class = "h">
          </div>
          <div class = "h">
            <h2>Control Panel</h2>
            <v-img style = "float: left; margin-right: 20px" src = "..\assets\guru.stucco.org.au_(iPad).png" width = "50%"></v-img>
            <p>
              The control panel was designed to work on wider displays, such as laptops, desktops and tablets. With in the control panel mode a user can perform a number of functions, given their status a user can edit or view the members in the database, their attendance and rent. Users can also write and submit minutes and attendance for a meeting. Minutes can be saved as a draft and will remain on a users profile until it is either sent or deleted. Minutes are checked for odd dates and quorum before being sent. Once sent the minutes are emailed to all residents and stored in the database, attendance is then automatically updated.
            </p>
          </div>
        </v-window-item>
        <v-window-item>Hello</v-window-item>
      </v-window>





        <v-textarea v-model = "p1" class = "txt"></v-textarea>
  </div>
</template>

<script>
import 'material-design-icons-iconfont/dist/material-design-icons.css'
let cssSet = (variable, set) => {document.documentElement.style.setProperty(variable, set);}
  export default {
    name: 'splashscreen',

    data: () => ({
      p1: '',
      pg: 0,
      pgs: 3

    }),
    methods: {
      next(direction){
        if(direction == 'left'){
          this.pg --;
        }else if(direction == 'right'){
          this.pg ++;
        }
        this.fade()
      },
      fade(){
        cssSet('--opacity', 1)
        setTimeout(()=>{
          cssSet('--opacity', 0);
        },1000)
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
.lctn div{
  border-radius: 50px;
  position: absolute;
  top: 0;
  left: 0;
  border: 12.5px solid rgba(240, 162, 81, 0.5);
  margin: -12px -12px;
  width: 50px;
  height: 50px;
  transition: 0.5s;
}
.lctn div:not(.show){
  opacity: 0;
}
.show{
  opacity: 1;
}
.lctn {
  position: relative;
  margin: 40px;
  width:26px;
  height:26px;
  padding: 12px;
  border-radius: 26px;
  background: rgb(240, 162, 81);
}
#about-guru{
  background: white;
  padding:  100px var(--padding);
  font-family: 'Roboto', sans-serif;
}
.bottom{
  position: fixed;
  bottom: 0;
  left: 0;
  z-index: 900;
  opacity: var(--opacity);
  transition: 0.7s;
}
.bottom:hover{
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
.left:hover, .right:hover{
  opacity: 1;
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
  font-size: 25px;
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
