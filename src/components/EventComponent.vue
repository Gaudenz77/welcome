 <!-- <template>
  <div class="container">
    <div class="row justify-content-evenly">
      <div class="selctionDropdown">
        <select v-model="selectedCategory">
          <option value="All">All Categories</option>
          <option value="education">{{ capitalizeFirstLetter('education') }}</option>
          <option value="food">{{ capitalizeFirstLetter('food') }}</option>
          <option value="general">{{ capitalizeFirstLetter('general') }}</option>
        </select>
      </div>
      <div class="col-12 m-3 infoBoxBs" v-for="(event, index) in filteredEvents" :key="index">
        <span class="m-3">
          <li class="list-group-item li-time">{{ event.eventDate}} / {{ event.eventTime }}</li>
          <li class="list-group-item li-topic">{{ event.eventTitle }}</li>
          <li class="list-group-item li-info">{{ event.eventInfo }}</li>
        </span>
      </div>
    </div>
  </div>
</template> -->

<template>
  <div class="selctionDropdown">
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
<!-- <script>
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
    applyFilter(filter) {
      this.filter = filter;
    },
    resetFilter() {
      this.filter = {
        food: false,
        education: false,
        general: false,
      };
      this.keywordFilter = '';
    },
  },
};
</script>  -->

<!-- Google API -->
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
      const spreadsheetId = '18mvQRLVuW2JPUQTZI0xkYAu8TEHzS1i2WlDPn-qht4Y';  // 10IMOzXvjDdecxgc9rc7dIXkn0q-4kOzkoVwqY_xjGc8 look above
      /* const range = 'Tabellenblatt1!A1:AA1000'; */ // Replace with the range of cells you want to retrieve
      const api_token = 'AIzaSyCywsxvpyfF4HeBJO1th1FHaPZ4pB77UHA';
      const url = `https://sheets.googleapis.com/v4/spreadsheets/${spreadsheetId}/values:batchGet?ranges=A1%3AE100&valueRenderOption=FORMATTED_VALUE&key=${api_token}`;
      axios
        .get(url)
        .then((response) => {
          console.log(response);
          const data = response.data.valueRanges[0].values
            .slice(1)
            .map((row) => ({
              eventTime: row[0],
              eventDate: row[1],
              eventTitle: row[2],
              eventInfo: row[3],
              eventCategory: row[4],
            }));
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
.infoBoxBs {
  background-color: #0F05A0;
  padding-left:25px;
}
.infoBox {
  width: 80%;
  margin: 0 auto;
  margin-top: 20px;
  width: 960px;
  height: 182px;
  background-color: #0f05a0;
  padding: 25px;
  text-decoration: none;
}
.li-time {
  font-family: 'Inter', sans-serif;
  font-size: 28px;
  font-weight: 900;
  color: #eb5e00;
  text-decoration: none;
}
.li-topic {
  font-family: 'Inter', sans-serif;
  font-size: 28px;
  font-weight: 900;
  color: #ffbfab;
  text-decoration: none;
}
.li-info {
  font-family: 'Inter', sans-serif;
  font-size: 28px;
  font-weight: 500;
  color: #ffbfab;
  text-decoration: none;
}
</style>