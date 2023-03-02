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