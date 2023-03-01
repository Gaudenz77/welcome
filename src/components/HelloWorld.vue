<template>
  <div class="conatiner-fluid">
    <div class="row">
      <div class="col"><h1>{{ msg }}</h1></div>
    </div>
  </div>
   
    <div class="container">
      <div class="row justify-content-evenly">
        <div class="col-md-3 bg-info m-3">Lorem ipsum dolor sit amet consectetur adipisicing elit. Praesentium est, dolorum temporibus, officiis quod deserunt eum voluptatum nobis quis quibusdam porro, ipsum harum reprehenderit. Sint ipsum perferendis illum animi voluptatibus?</div>
        <div class="col-md-3 bg-info m-3">Lorem ipsum dolor sit, amet consectetur adipisicing elit. Dignissimos deserunt id incidunt beatae odit aut. Ab nulla ea velit ducimus repellendus voluptate atque nostrum obcaecati amet perspiciatis, accusantium officiis eveniet?</div>
        <div class="col-md-3 bg-info m-3">Lorem ipsum dolor sit amet, consectetur adipisicing elit. Consectetur modi perferendis facere alias, culpa eos quae architecto itaque amet optio eveniet officia accusamus quos iusto perspiciatis provident enim, sint inventore.</div>
      </div>
    </div>
   
</template>

<script>
export default {
  name: 'HelloWorld',
  props: {
    msg: String
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
</style>
