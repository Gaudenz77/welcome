<!-- <template>
  <div class="container">
    <div class="row justify-content-evenly">
      <div><WelcomeToOpportunity msg="Welcome to Opportunity"/></div>
      <div class="col-12 m-3 infoBoxBs" v-for="(event, index) in events" :key="index">
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
  <div>
    <ul v-for="(event, index) in events" :key="index" class="infoBox">
      <li>
        <span class="li-time">{{ event.eventDate}} / {{ event.eventTime }}</span><br>
        <span class="li-topic">{{ event.eventTitle }}</span><br>
        <span class="li-info">{{ event.eventInfo }}</span>
      </li>
    </ul>
  </div>
</template>

<script>
import axios from 'axios';

export default {
  data() {
    return {
      events: [],
    };
  },
  mounted() {
    this.fetchData();
    setInterval(() => {
      this.fetchData();
    }, 1800000);
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
              const [eventTime, eventDate, eventTitle, eventInfo] = line.split(',');
              return { eventTime, eventDate, eventTitle, eventInfo };
            });
          this.events = data;
        })
        .catch((error) => {
          console.error(error);
        });
    },
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
