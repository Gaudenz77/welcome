<template>
    <div class="conatiner-fluid">
    <div class="row">
        <div class="col"><h1>{{ msg }}</h1></div>
        <p>{{currentDate()}}</p>
    </div>
  </div>
</template>
<script>
export default {
  name: 'WelcomeToOpportunity',
       
  props: {
    msg: String,
   
  },

  methods: {
    currentDate() {
      const current = new Date();
      const date = `${current.getDate()}/${current.getMonth()+1}/${current.getFullYear()}`;
      return date;
    }
  }
 

}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h1 {
    font-size: 60px;
    font-weight:bold;
    text-align:left;
}
h3 {
  margin: 40px 0 0;
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