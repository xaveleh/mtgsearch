<template>
<form @submit="cardSearch">
    <input type="search" v-model="cardName" placeholder="Search by card name..." />
    <input type="submit" value="Submit" />
</form>
</template>

<script>
export default {
    name: "SearchBar",
    data() {
        return {
            cardName: ''
        }
    },
    methods: {
        cardSearch(e) {
            e.preventDefault();
            const newSearchCard = {
                cardName: this.cardName
            }
            this.$emit('get-results', newSearchCard);
            this.cardName = '';
        }
    }
}
</script>