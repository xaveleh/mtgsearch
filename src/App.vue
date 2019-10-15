<template>
  <div id="app">
    <SearchBar v-on:get-results="getResults" />
    <ul>
      <li v-for="(card) in results" v-bind:key="card.id" id="cardinfo">
        {{card.name}}
        <em>{{card.setName}}</em>
        <img v-bind:src="card.imageUrl" />
        <ul v-for="(ruling) in card.rulings" v-bind:key="ruling.text">
          <li>
            {{ruling.text}}
          </li>
        </ul>
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
      results: [],
      rulings: []
    }
  },
  methods: {
    getResults(newSearchCard) {
      const { cardName, cardColor, setName, cardType } = newSearchCard;
      axios.get(`https://api.magicthegathering.io/v1/cards?name=${cardName}&colors=${cardColor}&setName=${setName}&types=${cardType}`)
      .then(res => {
        this.results = res.data.cards.filter(card => !!card.multiverseid)})
    },
  }
}
</script>

<style>
body {
  background: #e6ffec;
}
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
  margin: 2px;

}
#cardinfo {
  border-top: 1px dotted black;
  clear: both;
  text-align: left;
}
</style>
