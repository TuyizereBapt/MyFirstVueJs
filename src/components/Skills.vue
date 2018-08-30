<template>
  <div class="hello">
    <h1>{{ name }}</h1>
     <div>{{btnState? "The button is disabled":"The button is Active"}}</div>
    <button v-on:click="changeState" v-bind:disabled="btnState">Click Me {{btnState}}</button>
    <ul>
      <li v-for="(data,index) in skills" :key="index">{{index}}. {{data.skill}}</li>
    </ul>
    <p v-if="skills.length > 2">You have more than 2 Skills. Excellent.</p>
    <p v-else>You have less Skills. Keep going up.</p>
  </div>
</template>

<script>
export default {
  name: "Skills",
  data() {
    return {
      name: "Starting my first Vue Js App By Bapt Hey What is it you want",
      btnState: false,
      skills:[
        {"skill":"Vue.js"},
        {"skill":"Html"},
      ]
    };
  }
};
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
