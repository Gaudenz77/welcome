<div class="container">
    <div class="row">
      <div class="col-sm-12 bg-info m-3"></div>
      <div class="col-sm-12 bg-info m-3"></div>
      <div class="col-sm-12 bg-info m-3"></div>
    </div>
  </div>

'WelcomeToOpportunity'

<template>

  
</template>

<script>
/* WelcomeOpportunity.vue ln 28 -32
  data() {
    return {
      events: [],
    }
  } */


  export default {
    name: "app",
    data(){
      return {
};
    },
    methods: {

getDate(){
    
  },
  updateCurrentDate() {

  let current = new Date();
  this.currentDate = `${current.getDate()}.${current.getMonth()+1}.${current.getFullYear()}`;

  },

  refreshData() {
    this.updateCurrentDate();
    this.getDate();
  },
},
mounted() {
  this.refreshData();
  setInterval(this.refreshData,1800000)
},

};

</script>


<script>
/*   CEventcomponent without  Intrerval */
import axios from 'axios';
import { Script } from 'vm';

export default {
  data() {
    return {
      events: [],
    };
  },
  mounted() {
    axios
      .get(
        'https://docs.google.com/spreadsheets/d/e/2PACX-1vTWMQ1bHW9tkX0eeaIJOw-4fphuRuqwh8KvAoTpPut1JC72CZuaFSnUJEA7cgeNaEDI51YRdOW3V50D/pub?output=csv'
      )
      .then((response) => {
        const data = response.data.trim().split('\n').slice(1).map((line) => {
          const [eventDate, eventTitle, eventInfo] = line.split(',');
          return { eventDate, eventTitle, eventInfo };
        });
        this.events = data;
      })
      .catch((error) => {
        console.error(error);
      });
  },
};
</script>

<div class="btn-group" role="group" aria-label="Basic mixed styles example">
  <button type="button" class="btn btn-danger">Left</button>
  <button type="button" class="btn btn-warning">Middle</button>
  <button type="button" class="btn btn-success">Right</button>

  https://docs.google.com/spreadsheets/d/10IMOzXvjDdecxgc9rc7dIXkn0q-4kOzkoVwqY_xjGc8/edit?usp=sharing
  https://docs.google.com/spreadsheets/d/18mvQRLVuW2JPUQTZI0xkYAu8TEHzS1i2WlDPn-qht4Y/edit?usp=sharing
</div>

<div v-if="filteredEvents.length">
  <ul v-for="(event, index) in filteredEvents" :key="index" class="infoBox">
    <li>
      <span class="li-time">{{ event.eventDate}} / {{ event.eventTime }}</span><br>
      <span class="li-topic">{{ event.eventTitle }}</span><br>
      <span class="li-info">{{ event.eventInfo }}</span>
      <span hidden class="li-info">&nbsp;{{ event.eventCategory }}</span>
    </li>
  </ul>
</div>
<div v-else>
  <h2>No events currently listed.</h2>
</div>
</div>