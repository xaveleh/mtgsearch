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
            cardType: ''
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
                cardType: this.cardType
            }
            this.$emit('get-results', newSearchCard);
            this.cardName = '';
            this.cardColor = [];
            this.setName = '';
            this.inclusiveSearch = false;
            this.cardType = '';
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