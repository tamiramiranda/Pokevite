<script setup>
    const pokemon = defineProps(["name", "urlBaseSvg"])
</script>

<template>
    <div class="col-md-6 col-xl-4">
        <div class="card p-2 mb-3 cardListPokemon">
            <img :src="pokemon.urlBaseSvg + '.svg'" class="card-img-top" :alt="pokemon.name" height="80" />
            <p class="text-center">{{ pokemon.name }}</p>
        </div>
    </div>
</template>

<style scoped>
    .cardListPokemon{
        background: rgb(255,205,0);
        background: radial-gradient(circle, rgba(255,205,0,0.4682247899159664) 0%, rgba(219,136,0,1) 80%);
        cursor: pointer;
    }
    .cardListPokemon:hover{
        background: rgb(255,205,0);
        background: radial-gradient(circle, rgba(255,205,0,0.4682247899159664) 0%, rgba(242,150,0,1) 80%);
    }
    .cardListPokemon img:hover{
        padding: .1rem;
    }
    .cardListPokemon p{
        text-transform: capitalize;
        margin: 10px 0 0;
    }
</style>