<template>
    <div>
        <p v-on:get-results="getResults">{{results}}</p>
    </div>
</template>

<script>
import SearchBar from "./SearchBar";
export default {
    name: "Results",
    components: {
        SearchBar
    },
    data() {
        return {
            results: []
        }
    },
    methods: {
        getResults()
    }
}
</script>