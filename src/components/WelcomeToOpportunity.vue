<template>
  <div class="conatiner-fluid">
    <div class="row">
      <div class="titleWelcome">{{ msg }}</div>
      <h2 class="titleTimeDate">{{ currentDate }}</h2>
    </div>
  </div>
</template>
<script>

export default {
  name: 'WelcomeToOpportunity',
  props: {
    msg: String,
  },
  data() {
    return {
      currentDate: '',
    };
  },
  mounted() {
    this.updateDate();
    setInterval(() => {
      this.updateDate();
    }, 1800000);
  },
  methods: {
    updateDate() {
  const current = new Date();
  const date = `${current.getDate() < 10 ? "0" + current.getDate() : current.getDate()}.${(current.getMonth()+1) < 10 ? "0" + (current.getMonth()+1) : current.getMonth()+1}.${current.getFullYear()}`;
  this.currentDate = date;
}
  },
}

</script>


<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
/* h1 {
    font-size: 60px;
    font-weight:bold;
    text-align:left;
}
h3 {
  margin: 40px 0 0;
}
 */
.titleWelcome {
  font-family: 'Inter', sans-serif;
  font-size:62px;
  font-weight:900;
  margin-left:-10px; 
}


.titleTimeDate {
  font-family: 'Inter', sans-serif;
  font-size:62px;
  font-weight:500;
  color:#9AA7B1;
  text-decoration:none;
  margin-left:-10px; 
}
 
/*  ul {
  list-style-type: none;
  padding: 0;
}
 */

a {
  color: #42b983;
}
</style>