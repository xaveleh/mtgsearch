<template>
  <div id="app">
    <SearchBar v-on:get-results="getResults" />
    <ul>
      <li v-for="(card) in results" v-bind:key="card.id">
        {{card.name}}
        <img v-bind:src="card.imageUrl" />
      </li>
    </ul>
  </div>
</template>

<script>

import SearchBar from './components/SearchBar';
import axios from 'axios';

export default {
  name: 'app',
  components: {
    SearchBar
  },
  data() {
    return {
      results: []
    }
  },
  methods: {
    getResults(newSearchCard) {
      const { cardName } = newSearchCard;
      axios.get(`https://api.magicthegathering.io/v1/cards?name=${cardName}`)
      .then(res => {
        console.log(res);
        this.results = res.data.cards.filter(card => !!card.multiverseid)})
    },
  }
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
img {
  float: right;

}
li {
  border-bottom: 1px solid black;
  clear: both;
}
</style>
