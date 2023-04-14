<script setup>
    import PokemonCards from "./components/PokemonCards.vue"
</script>

<template>
    <main>
        <h1>Pokemon</h1>
        <Suspense>
            <template #default>
                <PokemonCards></PokemonCards>
            </template>
            <template #fallback>
                <div>
                    <p>loading...</p>
                </div>>
            </template>
        </Suspense>
    </main>
</template>