<template>
<form @submit="cardSearch">
    <input type="search" v-model="cardName" placeholder="Filter by card name..." />
    <input type="search" v-model="setName" placeholder="Filter by set name..." />
    <select v-model="cardType">
        <option selected="" value="" disabled>Filter by card type...</option>
        <option value="Artifact">Artifact</option>
        <option value="Creature">Creature</option>
        <option value="Enchantment">Enchantment</option>
        <option value="Instant">Instant</option>
        <option value="Land">Land</option>
        <option value="Planeswalker">Planeswalker</option>
        <option value="Sorcery">Sorcery</option>
        <option value="Tribal">Tribal</option>
    </select>
    <div id="multisearch">
        <label>Search for multicolor cards...</label>
        <input type="checkbox" value="inclusiveSearch" v-model="inclusiveSearch">
        <div v-if="inclusiveSearch">
            <input type="checkbox" v-model="cardColor" value="blue">
            <label>Blue</label>
            <input type="checkbox" v-model="cardColor" value="red">
            <label>Red</label>
            <input type="checkbox" v-model="cardColor" value="green">
            <label>Green</label>
            <input type="checkbox" v-model="cardColor" value="black">
            <label>Black</label>
            <input type="checkbox" v-model="cardColor" value="white">
            <label>White</label>
        </div>
    </div>
    <div id="checkboxes" v-if="!inclusiveSearch">
    <input type="checkbox" value="|blue|" v-model="cardColor">
    <label>Blue</label>
    <input type="checkbox" value="|red|" v-model="cardColor">
    <label>Red</label>
    <input type="checkbox" value="|green|" v-model="cardColor">
    <label>Green</label>
    <input type="checkbox" value="|black|" v-model="cardColor">
    <label>Black</label>
    <input type="checkbox" value="|white|" v-model="cardColor">
    <label>White</label>
    </div>
    <input type="submit" value="Submit" />
    <input type="button" @click="nextPage" value="Next Page">
    <input type="button" @click="prevPage" value="Previous Page" v-bind:disabled="pageNumber <= 1">
</form>
</template>

<script>
export default {
    name: "SearchBar",
    data() {
        return {
            cardName: '',
            cardColor: [],
            setName: '',
            inclusiveSearch: false,
            cardType: '',
            pageNumber: 1
        }
    },
    methods: {
        cardSearch(e) {
            e.preventDefault();
            const newSearchCard = {
                cardName: this.cardName,
                cardColor: this.cardColor,
                setName: this.setName,
                inclusiveSearch: this.inclusiveSearch,
                cardType: this.cardType,
                pageNumber: 1
            }
            this.$emit('get-results', newSearchCard);
            this.inclusiveSearch = false;
            this.cardName = this.cardName;
            this.cardColor = this.cardColor;
            this.setName = this.setName;
            this.cardType = this.cardType;
            this.pageNumber = 1;
        },
        nextPage(e) {
            e.preventDefault();
            const newSearchCard = {
                cardName: this.cardName,
                cardColor: this.cardColor,
                setName: this.setName,
                inclusiveSearch: this.inclusiveSearch,
                cardType: this.cardType,
                pageNumber: this.pageNumber += 1
            }
            this.$emit('next-page', newSearchCard);
            this.inclusiveSearch = false;
        },
        prevPage(e) {
            e.preventDefault();
            const newSearchCard = {
                cardName: this.cardName,
                cardColor: this.cardColor,
                setName: this.setName,
                inclusiveSearch: this.inclusiveSearch,
                cardType: this.cardType,
                pageNumber: this.pageNumber -= 1
            }
            this.$emit('prev-page', newSearchCard);
            this.inclusiveSearch = false;
        }
    }
}
</script>

<style scoped>
#multisearch {
    display: block;
}
input {
    margin:2px;
}

</style>