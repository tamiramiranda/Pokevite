<script setup>
  import { onMounted, computed, ref } from "vue";
  import ListPokemons from "../components/ListPokemons.vue"
  import CardPokeonSelected from "../components/CardPokemonSelected.vue"

  let pokemons = ref();
  let urlBaseSvg = ref("https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/other/dream-world/");
  let searchPokemonField = ref();
  let pokemonSelected = ref();
  let loading = ref(false)

  onMounted(() => {
    fetch("https://pokeapi.co/api/v2/pokemon?limit=151&offset=0")
    .then(res => res.json())
    .then(res => pokemons.value = res.results)
    .catch(err => alert("Erro ao realizar a consulta!"))
  })

  const pokemonsFiltered = computed(() => {
    if(pokemons.value && searchPokemonField.value){
      return pokemons.value.filter(pokemon => (
        pokemon.name.toLowerCase().includes(searchPokemonField.value.toLowerCase())
      ));
    }
    return pokemons.value;
  })

  const selectPokemon = async (pokemon) => {
    loading.value = true;
    await fetch(pokemon.url)
    .then(res => res.json())
    .then(res => pokemonSelected.value = res)
    .catch(err => alert(err))
    .finally(() => loading.value = false)
  }

</script>

<template>
  <main>
    <div class="container">

      <div class="row mt-4">
        <div class="col-sm-12 col-md-6">
          <CardPokeonSelected
            :name="pokemonSelected?.name"
            :xp="pokemonSelected?.base_experience"
            :height="pokemonSelected?.height"
            :url="pokemonSelected?.sprites.other.dream_world.front_default"
            :loading="loading"
          />
        </div>

        <div class="col-sm-12 col-md-6">
          <div class="card card-list">
            <div class="card-body row">

              <div class="mb-3">

                <label
                  hidden
                  for="searchPokemonField"
                  class="form-label">
                  Pesquisar...
                </label>

                <input
                  type="text"
                  class="form-control"
                  id="searchPokemonField"
                  placeholder="Pesquisar..."
                  v-model="searchPokemonField"
                >

              </div>

              <ListPokemons
                v-for="(pokemon, index) in pokemonsFiltered"
                :key="index"
                :name="pokemon.name"
                :urlBaseSvg="urlBaseSvg + pokemon.url.split('/')[6]"
                @click="selectPokemon(pokemon)"
              />

            </div>
          </div>
        </div>
      </div>

    </div>
  </main>
</template>

<style scoped>
  .card-list{
    max-height: 75vh;
    overflow-y: scroll;
    overflow-x: hidden;
  }

  @media (max-width: 768px) {
    .card-list{
      max-height: 48vh;
    }
  }
</style>