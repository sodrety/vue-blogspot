<template>
  <img alt="Vue logo" src="./assets/logo.png" />
  <HelloWorld :msg="messages"/>
  <!-- <Coba text="Cooook"/> -->
  <input type="text" v-model="messages" />
  <button @click="alertMessage">Alert</button>
  <div>
    <ul>
      <li v-for="list in lists" v-bind:key="list">{{ list.title }}</li>
    </ul>
  </div>
</template>

<script>
import axios from 'axios';
import _ from 'lodash'
import HelloWorld from "./components/HelloWorld.vue";
// import Coba from "./components/Coba.vue";

export default {
  name: "App",
  components: {
    HelloWorld,
    // Coba
  },
  
  data(){
    return {
      messages: 'Hello World Cuuuuk!'
    }
  },

  methods: {
    alertMessage(){
      alert(this.messages)
    }
  },

  created() {
    axios.get(`http://jsonplaceholder.typicode.com/posts`)
    .then(response => {
      this.lists = _.slice(response.data,0,5)
    })
    .catch(e => {
      this.errors.push(e)
    })
  }
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
