<template>
  <div>
    <!-- formulario de busqueda -->
    <div class="container mt-4">
      <div class="d-flex justify-content-center my-5">
        <h1>Pokedex</h1>
        <img src="https://img.icons8.com/ios-glyphs/60/FFFFFF/pokeball.png" />
      </div>

      <div class="container d-flex justify-content-center">
        <form v-on:submit.prevent="listPokemon">
          <div class="input-group mb-3">
            <input
              type="text"
              class="form-control input-w"
              placeholder="Ingrese el Nombre del Pokemon"
              aria-label="Recipient's username"
              aria-describedby="button-addon2"
              v-model="pokemon.name"
            />
            <button
              class="btn btn-outline-light"
              type="submit"
              @click="listPokemon"
            >
              Buscar Pokemon
            </button>
          </div>
        </form>
      </div>
    </div>
    <div class="container my-3">
      <div class="row">
        <div class="col-12 text-center my-3">
          <h2>Nombre pokemon : {{ pokemon.name }}</h2>
        </div>
        <div class="col-2">
          <img :src="fotoPokemon" alt="pokemon" class="pokemonImg" />
        </div>
        <div class="col-5">
          <h2 class="text-center">habilidades</h2>
          <ul v-for="habilidad in habilidades" :key="habilidad">
            <li>{{ habilidad.ability.name }}</li>
          </ul>
        </div>
        <div class="col-5">
          <h2 class="text-center">movimientos</h2>
          <div class="scroll overflow-auto bg-dark">
            <ul v-for="movimiento in movimientos" :key="movimiento">
            <li>{{ movimiento.move.name }}</li>
          </ul>
          </div>
        </div>
      </div>
    </div>
  </div>
  <HelloWorld />
</template>

<script>
import HelloWorld from "./components/HelloWorld.vue";

export default {
  name: "App",
  data() {
    return {
      pokemon: {
        name: "pikachu",
        sprites: {
          front_default: "",
        },
        moves: [],
        abilities: [],
      },
    };
  },
  created() {
    this.listPokemon();
  },
  methods: {
    listPokemon: async function () {
      try {
        const res = await fetch(
          `https://pokeapi.co/api/v2/pokemon/` + this.pokemon.name
        );
        const data = await res.json();
        this.pokemon = data;
        console.log(this.pokemon);
      } catch (error) {
        console.log(error);
      }
    },
  },
  computed: {
    fotoPokemon() {
      return this.pokemon.sprites.front_default;
    },
    habilidades() {
      return this.pokemon.abilities;
    },
    movimientos() {
      return this.pokemon.moves;
    },
  },
  components: {
    HelloWorld,
  },
};
</script>
 
<style>
body{
  background-image: url("https://img.wallpapersafari.com/desktop/1366/768/9/71/GfXWN8.jpg");
  background-repeat: no-repeat;
  background-size: cover;
  
}
.container{
  color: white;
}
.pokemonImg {
  width: 100%;
}
.scroll{
  height: 150px;
}

</style>
