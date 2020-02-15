<template>
  <div id = "about-guru">
        <h1>Backstory</h1>
        <p>
          As a resident of the Sydney University Student Cooperative (Stucco), I would often lose my key, a small NFC chip. I was not the only one that did this, many fellow residents would also misplace their key or simply forget to bring it on short trips. As a self-taught web developer and student of engineering mechatronics, I decided to develop a solution to the problem at hand. I was able to develop a single page web application that could allow residents to unlock the doors. The implementation of Guru was approved, provided that security protocols where put in place. Guru was a great success with all residents joining the user database and half choosing Guru over the physical key. As Guru became a bookmark or forever open tab on most people's phones, as well as a database with profiles for each resident, I began to develop other functions to aid in general admin and solve problems other residents and committees where having. For instance, before Guru Minute's residents would write minutes in any form of a text editor and then send the minutes to a google group. They would then have to find the link to a google form and tick all residents and applicants who attended the meeting. This tortuous process often led to attendance being overlooked and irregular formatting of minutes.
        </p>

        <h1>What is Guru</h1>
        <p>
          As a resident of the Sydney University Student Cooperative (Stucco), I would often lose my key, a small NFC chip. I was not the only one that did this, many fellow residents would also misplace their key or simply forget to bring it on short trips. As a self-taught web developer and student of engineering mechatronics, I decided to develop a solution to the problem at hand. I was able to develop a single page web application that could allow residents to unlock the doors. The implementation of Guru was approved, provided that security protocols where put in place. Guru was a great success with all residents joining the user database and half choosing Guru over the physical key. As Guru became a bookmark or forever open tab on most people's phones, as well as a database with profiles for each resident, I began to develop other functions to aid in general admin and solve problems other residents and committees where having. For instance, before Guru Minute's residents would write minutes in any form of a text editor and then send the minutes to a google group. They would then have to find the link to a google form and tick all residents and applicants who attended the meeting. This tortuous process often led to attendance being overlooked and irregular formatting of minutes.
        </p>
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

#about-guru{
  background: white;
  padding: 150px;
  font-family: 'Roboto', sans-serif;
}
h1{
  font-size: 70px;
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

</style>
