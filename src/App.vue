<template>
  <div id="app">
    <Header></Header>
    <Titol></Titol>
    <div class="out">
      <div class="warning">
        <h1 v-if="warns != null">Hi ha {{warns}} models amb problemes d'estoc</h1>
        <div  v-for= "model in models" :key="model.id">
          <Model v-if="model.warn == true" v-bind:name="model.name" v-bind:warn="model.warn" v-bind:id ="model.id"></Model>
        </div>
      </div>
      <div class="search_bar">
        <h1> Cercador de models </h1>
        <input class="search text" type="text" id="search_bar" v-on:keypress=getModelsBySearch() />
      </div>
      <div class="warning">
        <div v-for= "search in searchs" :key="search.id">
          <Model v-bind:name="search.name" v-bind:warn="search.warn" v-bind:id ="search.id"></Model>
        </div>
      </div>
    </div>  
  </div>
</template>

<script>
import Header from './components/Header.vue'
import Titol from './components/Titol.vue'
import Model from './components/Model.vue'
import axios from 'axios'

export default {
  name: 'App',
  components: {
    Header,
    Titol,
    Model,
  },
  data() {
    return {
      models: [],
      searchs: [],
      warns: null,
      search: '',
    }
  },
  mounted() {
    console.log('App mounted.')
    this.getModels();
  },
  methods: {
    async getModels() {
      axios.get('http://34.134.230.81/models/')
        .then(response => {
          this.warns = response.data["total_warns"]
          this.models = response.data["models"];
          console.log(this.models);
        })
        .catch(e => {
          console.log(e);
        })
    },
    async getModelsBySearch() {
      axios.get('http://34.134.230.81/models?query=' + document.getElementById('search_bar').value)
        .then(response => {
          this.searchs = response.data.models;
          console.log(this.searchs);
        })
        .catch(e => {
          console.log(e);
        })
    }
  }
}
</script>

<style>
@import './assets/css/style.css';


</style>