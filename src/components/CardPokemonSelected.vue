<script setup>
    const pokemon = defineProps(["name", "url", "xp", "height", "loading"])
</script>

<template>
    <div
        class="card CardPokemonSelected"
        :class="loading ? '' : 'animate__animated animate__flipInY'"
    >
        <template v-if="pokemon.url">
            <img :src="pokemon.url" alt="{{ pokemon.name }}" />
        </template>
        <template v-else>
            <img src="../assets/egg_pokemon.svg" alt="???" />
        </template>

        <div>
            <h5 class="card-title text-center">{{ pokemon.name ? pokemon.name : "???" }}</h5>
            <div class="row text-center" v-if="pokemon.xp || pokemon.height">
                <section>
                    <strong>XP: </strong>
                    <span>{{ pokemon.xp }}</span>
                </section>
                <section>
                    <strong>Altura: </strong>
                    <span>{{ pokemon.height }}</span>
                </section>
            </div>
        </div>

    </div>
</template>


<style scoped>
    .CardPokemonSelected{
        height: 75vh;
        background: rgb(255,205,0);
        background: radial-gradient(circle, rgba(255,205,0,0.4682247899159664) 0%, rgba(219,136,0,1) 80%);
        display: flex;
        justify-content: center;
    }
    .CardPokemonSelected img{
        height: 250px;
    }
    .CardPokemonSelected h5{
        text-transform: capitalize;
        margin-top: 30px;
    }
    @media (max-width: 768px) {
        .CardPokemonSelected{
            height: 30vh;
            width: 50%;
            margin: 0 auto 10px auto;
        }
        .CardPokemonSelected img{
            height: 100px;
        }
    }
</style>