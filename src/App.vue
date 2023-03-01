<template>
<img alt="Vue logo" src="./assets/logo.png" style="width:10%;">@
<!-- <i class="fa-solid fa-at fa-5x" style="color:black;"></i> -->
<img alt="Vue logo" src="./assets/Opportunity.png">
<!-- <HelloWorld msg="Welcome to Your Vue.js App"/> -->
  <!-- <WelcomeToOpportunity msg="Welcome to Opportunity"/> -->

  <div class="container">
      <div class="row justify-content-evenly">
        <div><WelcomeToOpportunity msg="Welcome to Opportunity"/></div>
        <div class="col-12 m-3 infoBoxBs">
          <span class="m-3 px-2">
              <li class="list-group-item li-time">{{ currentdate }}19:30 Uhr</li>
              <li class="list-group-item li-topic">{{ title }}Besuch</li>
              <li class="list-group-item li-time">{{ info }}Interessierte können uns gerne für den zweiten Kurs besuchen</li>
              </span></div>
        <div class="col-12 m-3 infoBoxBs">
          <span class="m-3 px-2">
              <li class="list-group-item li-time">{{ currentdate }}19:30 Uhr</li>
              <li class="list-group-item li-topic">{{ title }}Besuch</li>
              <li class="list-group-item li-info">{{ info }}Interessierte können uns gerne für den zweiten Kurs besuchen</li>
              </span></div>
        <div class="col-12 m-3 infoBoxBs">
          <span class="m-3 px-2">
              <li class="list-group-item li-time">{{ currentdate }}19:30 Uhr</li>
              <li class="list-group-item li-topic">{{ title }}Besuch</li>
              <li class="list-group-item li-info">{{ info }}Interessierte können uns gerne für den zweiten Kurs besuchen</li>
              </span></div>
      </div>
    </div>



  <div class="container">
    <div class="row">
      <div class="col">
        <div  id="titleOriginal"><WelcomeToOpportunity msg="Welcome to Opportunity"/></div>
            <ul class="infoBox">           
              <li class="">
              <span class="li-time">{{ currentdate }}19:30 Uhr</span><br>
              <span class="li-topic">{{ title }}Besuch</span><br>
              <span class="li-info">{{ info }}Interessierte können uns gerne für den zweiten Kurs besuchen</span>
              </li>
            </ul>
            <ul class="infoBox">   
              <li class="">
              <span class="li-time">{{ currentdate }}19:30 Uhr</span><br>
              <span class="li-topic">{{ title }}Besuch</span><br>
              <span class="li-info">{{ info }}Interessierte können uns gerne für den zweiten Kurs besuchen</span>
            </li>
          </ul>
      </div>
    </div>
  </div>

    
  <footer>
    <div class="footer-wrapper">
      <div class="footer-item">
        <img src="./assets/STZH_SEB_Logo.png" alt="Image 1">
      </div>
      <div class="footer-item">
        <img src="./assets/Opportunity.png" alt="Image 2">
      </div>
      <div class="footer-item">
        <img src="./assets/SAG_Logo_De.png" alt="Image 3">
      </div>
    </div>
  </footer>

</template>

<script>
/* import HelloWorld from './components/HelloWorld.vue' */
import WelcomeToOpportunity from './components//WelcomeToOpportunity.vue'

export default {
  name: 'App',
  components: {
    /* HelloWorld, */
    WelcomeToOpportunity,
    
  }
}
</script>

<style>
#app {
  /* font-family: Avenir, Helvetica, Arial, sans-serif; */
  font-family: 'Inter', sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  /* text-align: center; */
  /* color: #2c3e50;
  margin-top: 60px; */
}



body {
  margin-bottom:40vh;
}

#titleOriginal {
position: absolute;
left:166px;
margin-top:-200px;



}

.infoBoxBs {
  background-color: #0F05A0;

}


.infoBox {
  width:80%;
  margin: 0 auto;
  margin-top:20px;
  height:fit-content;
  background-color: #0F05A0;
  padding:20px;
  text-decoration:none;

}



.li-time {
  font-family: 'Inter', sans-serif;
  font-size:28px;
  font-weight:900;
  color:#EB5E00;
  
  
}

.li-topic {
  font-family: 'Inter', sans-serif;
  font-size:28px;
  font-weight:900;
  color:#FFBFAB;
  text-decoration:none;
  

}

.li-info {
  font-family: 'Inter', sans-serif;
  font-size:28px;
  font-weight:500;
  color:#FFBFAB;
  

}

footer {
  background-color:white;
  padding: 20px;
  position:fixed;
  bottom: 0;
  z-index: 1;
  
}

.footer-wrapper {
  display: flex;
  justify-content: space-between;
  align-items: center;
  max-width: 100%;
  margin: 0 auto;
}

.footer-item {
  flex-basis: calc(33.33% - 20px);
  text-align: center;
}

.footer-item img {
  max-width: 100%;
}


ul {
  list-style: none;
}

</style>
