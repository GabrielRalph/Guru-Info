<template>
  <div id = "about-guru">

      <div class = "h">
        <h1>Backstory</h1>
        <p>
          As a resident of the Sydney University Student Cooperative (Stucco), I would often lose my key, a small NFC chip. I was not the only one that did this, many fellow residents would also misplace their key or simply forget to bring it on short trips. As a self-taught web developer and student of engineering mechatronics, I decided to develop a solution to the problem at hand. I was able to develop a single page web application that could allow residents to unlock the doors. The implementation of Guru was approved, provided that security protocols where put in place. Guru was a great success with all residents joining the user database and half choosing Guru over the physical key. As Guru became a bookmark or forever open tab on most people's phones, as well as a database with profiles for each resident, I began to develop other functions to aid in general admin and solve problems other residents and committees where having. For instance, before Guru Minute's residents would write minutes in any form of a text editor and then send the minutes to a google group. They would then have to find the link to a google form and tick all residents and applicants who attended the meeting. This tortuous process often led to attendance being overlooked and irregular formatting of minutes.
        </p>
      </div>

      <div class = "h">
        <h1>What is Guru</h1>
        <p>
          Guru is a web application to help residents of student housing with general admin organization and opening doors. Guru has been designed to work in two main modes. Guru will automatically choose the mode based on the users device and screen aspect ratio.
          <br /><br />
        </p>
        <h2>Dashboard</h2>
        <div class = "sc-phone">
          <div>
            <img src = "../assets/front.svg"/>
          </div>
          <div>
            <img src = "../assets/back.svg"/>
          </div>
        </div>
        <p>
          The mobile dashboard was designed specifically for mobile phones and can be added to the home screen on most mobile handsets.  The mobile dashboard allows users to unlock a given door by tapping on its icon. This will unlock the door for 4 seconds before locking again. Users can also view relevant information such as their rent balance, dates of meetings and attendance respectively.
          <br /><br />
        </p>
      </div>
      <div class = "h">
        <h2>Control Panel</h2>
        <v-img style = "float: left; margin-right: 20px" src = "..\assets\guru.stucco.org.au_(iPad).png" width = "50%"></v-img>
        <p>
          The control panel was designed to work on wider displays, such as laptops, desktops and tablets. With in the control panel mode a user can perform a number of functions, given their status a user can edit or view the members in the database, their attendance and rent. Users can also write and submit minutes and attendance for a meeting. Minutes can be saved as a draft and will remain on a users profile until it is either sent or deleted. Minutes are checked for odd dates and quorum before being sent. Once sent the minutes are emailed to all residents and stored in the database, attendance is then automatically updated.
        </p>
      </div>




        <v-textarea v-model = "p1" class = "txt"></v-textarea>
  </div>
</template>

<script>
  export default {
    name: 'splashscreen',

    data: () => ({
      p1: ''
    }),

  }
</script>

<style>
@import url('https://fonts.googleapis.com/css?family=Roboto:300,300i,400,400i,500,500i,700,700i,900,900i&display=swap');
:root{
  --fact: 0.5;
}
#about-guru{
  background: white;
  padding: 150px;
  font-family: 'Roboto', sans-serif;
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
  width: calc(28vh * var(--fact));
  background-image: url('../assets/guru.stucco.org.au_(iPhone 6_7_8).png');
  background-size: 100%;
  height: calc(57.6vh  * var(--fact));
  float: right;
  margin:  0 0 20px 20px ;
  position: relative;
}
.sc-phone div{
  height: calc(12.4vh * var(--fact));
  position: absolute;
  top: calc(9.12vh * var(--fact));
  left: calc(4.24vh * var(--fact));
  perspective: 1000px;
}
.sc-phone div:last-of-type{
  left: calc(12.8vh * var(--fact));
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
