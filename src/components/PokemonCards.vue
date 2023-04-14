<script setup>
    import axios from "axios";
    import { ref, watch } from "vue";
    import Card from "./Card.vue"

    const pokemon = ref(null)
    const page = ref(0);

    const response = await axios.get("https://pokeapi.co/api/v2/pokemon?limit=8");
    pokemon.value = response.data.results;

    watch(page, async () => {
        const res = await axios.get(`https://pokeapi.co/api/v2/pokemon?limit=8&offset=${page.value * 8}`)
        pokemon.value = res.data.results;
    })
</script>

<template>
    <div class="container">
        <div class="cards">
            <Card v-for="mon in pokemon" :key="mon.name"
            :name="mon.name"
            :url="mon.url"></Card>
        </div>
        <div class="button-container">
            <button @click="page--">&lt</button>
            <button @click="page++">></button>
        </div>
    </div>
</template>

<style scoped>
.container {
    background-color: rgb(27, 26, 26);
    padding: 30px
}

.cards {
    max-width: 1000px;
    margin: 0 auto;
    display: flex;
    flex-wrap: wrap;
    height: 700px
}

.cards h3 {
    font-weight: bold;
}

.cards p {
    font-size: 10px;
}

.button-container {
    display: flex;
    justify-content: center;
    padding-top: 30px
}

.button-container button {
    border: none;
    width: 50px;
    height: 50px;
    border-radius: 100%;
    margin: 0 5px;
    cursor: pointer;
}
</style>