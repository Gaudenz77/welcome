<!-- <div class="container">
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


import axios from 'axios';
import EventFilter from '@/components/EventFilter.vue';

export default {
  components: {
    EventFilter,
  },
  data() {
    return {
      events: [],
      filter: {
        food: false,
        education: false,
        general: false,
      },
      keywordFilter: '',
    };
  },
  mounted() {
    this.fetchData();
    setInterval(() => {
      this.fetchData();
    }, 1800000);
  },
  computed: {
    filteredEvents() {
      if (this.filter.food || this.filter.education || this.filter.general || this.keywordFilter) {
        return this.events.filter((event) => {
          const matchesCategory = (!this.filter.food || event.eventCategory !== 'food') &&
            (!this.filter.education || event.eventCategory !== 'education') &&
            (!this.filter.general || event.eventCategory !== 'general');
          const matchesKeyword = !this.keywordFilter || event.eventInfo.toLowerCase().includes(this.keywordFilter.toLowerCase());
          return matchesCategory && matchesKeyword;
        });
      }
      return this.events;
    },
  },


  export default {
  data() {
    return {
      filter: {
      food: false,
      education: false,
      general: false,
    },
    searchText: "",
  };
  },
  computed: {
    filteredEvents() {
      return this.events.filter((event) => {
        const matchesSearchText = event.name
          .toLowerCase()
          .includes(this.searchText.toLowerCase());
        const matchesFilter =
          (this.filter.food && event.category === "food") ||
          (this.filter.education && event.category === "education") ||
          (this.filter.general && event.category === "general");
        return matchesSearchText && matchesFilter;
      });
    },
    },

    <div class="col-12 m-3  infoBox" v-if="filteredEvents.length">
        <ul v-for="(event, index) in filteredEvents" :key="index" class="infoBox">
          <span class="li-time">{{ event.eventDate}} / {{ event.eventTime }}</span><br>
          <span class="li-topic">{{ event.eventTitle }}</span><br>
          <span class="li-info">{{ event.eventInfo }}</span><br>
          <span hidden class="li-info">&nbsp;{{ event.eventCategory }}</span>
        </div>
      </div>
        <div v-else>
          <h2>No events currently listed.</h2>
        </div> -->


<!-- Variant Google-Csv shet export, non bootstrap, selectdropdown does NOT WORK! -->
  <!--
 <template>
  <div class="selectionDropdown">
    <select v-model="selectedCategory">
      <option value="All">All Categories</option>
      <option value="education">{{ capitalizeFirstLetter('education') }}</option>
      <option value="food">{{ capitalizeFirstLetter('food') }}</option>
      <option value="general">{{ capitalizeFirstLetter('general') }}</option>
    </select>
  </div>
  <div>
    <div v-if="filteredEvents.length">  
    <ul v-for="(event, index) in filteredEvents" :key="index" class="infoBox">
        <span class="li-time">{{ event.eventDate}} / {{ event.eventTime }}</span><br>
        <span class="li-topic">{{ event.eventTitle }}</span><br>
        <span class="li-info">{{ event.eventInfo }}</span><br>
        <span hidden class="li-info">&nbsp;{{ event.eventCategory }}</span>
    </ul>
    </div>
    <div v-else>
      <h2>No events currently listed.</h2>
    </div>
  </div>
</template>
<script>
import axios from 'axios';
export default {
  data() {
    return {
      events: [],
      selectedCategory: "All",
    };
  },
  mounted() {
    this.fetchData();
    setInterval(() => {
      this.fetchData();
    }, 1800000);
  },
  computed: {
    filteredEvents() {
  const currentTime = new Date().toLocaleTimeString('en-US', {hour12: false, hour: '2-digit', minute:'2-digit'});
  const filteredEvents = this.events.filter(event => {
    if (this.selectedCategory === "All") {
      return event.eventTime >= currentTime;
    } else {
      return (
        event.eventCategory === this.selectedCategory &&
        event.eventTime >= currentTime
      );
    }
  });
  return filteredEvents;
    }
  },
  methods: {
    fetchData() {
      axios
        .get(
          'https://docs.google.com/spreadsheets/d/e/2PACX-1vTWMQ1bHW9tkX0eeaIJOw-4fphuRuqwh8KvAoTpPut1JC72CZuaFSnUJEA7cgeNaEDI51YRdOW3V50D/pub?output=csv'
        )
        .then((response) => {
          const data = response.data
            .trim()
            .split('\n')
            .slice(1)
            .map((line) => {
              const [eventTime, eventDate, eventTitle, eventInfo, eventCategory] = line.split(',');
              return { eventTime, eventDate, eventTitle, eventInfo, eventCategory };
            });
          this.events = data;
        })
        .catch((error) => {
          console.error(error);
        });
    },
    capitalizeFirstLetter(str) {
    return str.charAt(0).toUpperCase() + str.slice(1);
  }
  },
};
</script> 

<style>
/* .infoBox {
  width: 80%;
  margin: 0 auto;
  margin-top: 20px;
  width: 960px;
  height: 182px;
  background-color: #0f05a0;
  padding: 25px;
  text-decoration: none;
} */</style>--> 