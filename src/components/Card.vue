<script setup>
    import axios from 'axios';
    import { defineProps, ref } from 'vue';

    const pokeAbilities = ref(null);
    const image = ref(null);
    const { name, url } = defineProps([
        'name',
        'url'
    ]);

    const response = await axios.get(url);
    pokeAbilities.value = response.data.abilities;
    image.value = response.data.sprites.front_default;
</script>

<template>
    <n-card>
    <template #cover>
        <img :src="image">
    </template>
    <h3>{{ name }}</h3>
    <div class="ability" v-for="abilities in pokeAbilities">
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

.ability {
    display: flex;
    flex-wrap: wrap;
}
</style>