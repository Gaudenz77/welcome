<template>
  <div>
    <ul v-for="(event, index) in events" :key="index" class="infoBox">
      <li>
        <span class="li-time">{{ event.eventDate }}</span><br>
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

<style>
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
}
</style>
