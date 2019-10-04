<template>
<form @submit="cardSearch">
    <input type="search" v-model="cardName" placeholder="Search by card name..." />
    <select v-model="cardColor" placeholder="Search by card color...">
        <option value="blue">Blue</option>
        <option value="red">Red</option>
        <option value="green">Green</option>
        <option value="black">Black</option>
        <option value="white">White</option>
    </select>
    <input type="submit" value="Submit" />
</form>
</template>

<script>
export default {
    name: "SearchBar",
    data() {
        return {
            cardName: '',
            cardColor: ''
        }
    },
    methods: {
        cardSearch(e) {
            e.preventDefault();
            const newSearchCard = {
                cardName: this.cardName,
                cardColor: this.cardColor
            }
            this.$emit('get-results', newSearchCard);
            this.cardName = '';
            this.cardColor = '';
        }
    }
}
</script>