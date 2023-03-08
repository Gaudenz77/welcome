<template>
      <div>
        <div class="col-sm mx-3">
          <select v-model="selectedCategory" class="form-select form-select-lg mt-3 mb-3 text-center" aria-label=".form-select-lg example" style="width:70%;">
            <option value="All">All Categories</option>
            <option value="education">{{ capitalizeFirstLetter('education') }}</option>
            <option value="food">{{ capitalizeFirstLetter('food') }}</option>
            <option value="general">{{ capitalizeFirstLetter('general') }}</option>
          </select>
        </div>
        <div v-if="filteredEvents.length"> 
          <ul class="col mx-3 my-5 p-4 infoBoxBs" v-for="(event, index) in filteredEvents" :key="index">
              <span class="li-time">{{ event.eventDate}} / {{ event.eventTime }}</span><br>
              <span class="li-topic">{{ event.eventTitle }}</span><br>
              <span class="li-info">{{ event.eventInfo }}</span><br>
              <span hidden class="li-info">&nbsp;{{ event.eventCategory }}</span>
          </ul>
        </div>
        <div v-else><h2>No events currently listed.</h2></div>
      </div>
</template>

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
      const api_token = 'AIzaSyCywsxvpyfF4HeBJO1th1FHaPZ4pB77UHA';
      const url = `https://sheets.googleapis.com/v4/spreadsheets/${spreadsheetId}/values:batchGet?ranges=A1%3AE100&valueRenderOption=FORMATTED_VALUE&key=${api_token}`;
      axios
        .get(url)
        .then((response) => {
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