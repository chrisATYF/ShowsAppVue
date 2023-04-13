<script setup>
    import axios from 'axios';
    import { defineProps, ref, watch } from 'vue';

    const pokeAbilities = ref(null);
    const pokeSprites = ref(null);
    const { name, url } = defineProps([
        'name',
        'url'
    ]);

    const response = await axios.get(url);
    pokeAbilities.value = response.data.abilities;
    pokeSprites.value = response.data.sprites.front_default;

    console.log(pokeSprites.value)
</script>

<template>
    <n-card>
    <template #cover>
        <img :src="pokeSprites">
    </template>
    <h3>{{ name }}</h3>
    <div class="jobs" v-for="abilities in pokeAbilities">
        <p v-for="ability in abilities">{{ability.name}}</p>
    </div>
  </n-card>
</template>

<style scoped>
.n-card {
    width: 200px;
    margin:10px 20px;
}
.n-card img {
    height: 250px
}

p {
    font-size: 10px;
}

.jobs {
    display: flex;
    flex-wrap: wrap;
}
</style>