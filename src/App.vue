<template>
  <div id="app">
    <router-view/>
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
      const { cardName, cardColor, setName, cardType, pageNumber } = newSearchCard;
      axios.get(`https://api.magicthegathering.io/v1/cards?name=${cardName}&colors=${cardColor}&setName=${setName}&types=${cardType}&page=${pageNumber}&pageSize=20`)
      .then(res => {
        this.results = res.data.cards.filter(card => !!card.multiverseid)})
    },
    nextPage(newSearchCard) {
      const { cardName, cardColor, setName, cardType, pageNumber } = newSearchCard;
      this.results = [{
        name: "Loading..."
      }];
      axios.get(`https://api.magicthegathering.io/v1/cards?name=${cardName}&colors=${cardColor}&setName=${setName}&types=${cardType}&page=${pageNumber}&pageSize=20`)
      .then(res => {
        this.results = res.data.cards.filter(card => !!card.multiverseid)})
         if(this.results.length < 1) {
          alert("Sorry, no more results to display!");
         }
    },
    prevPage(newSearchCard) {
      const { cardName, cardColor, setName, cardType, pageNumber } = newSearchCard;
      this.results = [{
        name: "Loading..."
      }];
      axios.get(`https://api.magicthegathering.io/v1/cards?name=${cardName}&colors=${cardColor}&setName=${setName}&types=${cardType}&page=${pageNumber}&pageSize=20`)
      .then(res => {
        this.results = res.data.cards.filter(card => !!card.multiverseid)})
    }
  }
}
</script>

<style>
body {
  background: #191a21;
}
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: white;
  margin-top: 60px;
}
img {
  float: right;
  margin: 2px;

}
#cardinfo {
  border-top: 1px dotted white;
  clear: both;
  text-align: left;
}
ul {
  color: white;
}
</style>
