<template>
  <div id="app">
    <div id="header">
      <img src="./assets/banner_pokedex(1).png" />
    </div>
    <div class="pesquisar">
      <input class="input is-normal" type="text" placeholder="Pesquisar">
      <label class="label"
        >Use a pesquisa avançada para explorar Pokémon por tipo, fraqueza,
        habilidade e mais!</label
      >
    </div>
    <div class="Sel">
      <div class="select is-danger is-loading">
        <select>
          <option>Crescente</option>
          <option>Decrescente</option>
          <option>A - Z</option>
          <option>Z - A</option>
        </select>
      </div>
    </div>
    <div class="columns is-multiline">
      <div v-for="(poke, index) in pokemons" :key="index" class="column is-3">
        <Pokemon :name="poke.name" :url="poke.url" :num="index + 1" />
      </div>
    </div>
    <div class="paginacao">
      <nav
        class="pagination is-medium is-rounded is-centered"
        role="navigation"
        aria-label="pagination"
      >
        <a class="pagination-previous" style="margin-left: 320px;">Próxima</a>
        <a class="pagination-next" style="margin-right: 370px;">Anterior</a>
        <ul class="pagination-list">
          <li><a class="pagination-link" aria-label="Goto page 1">1</a></li>
          <li><a class="pagination-link" aria-label="Goto page 2">2</a></li>
          <li>
            <a class="pagination-link" aria-label="Page 3" aria-current="page"
              >3</a
            >
          </li>
          <li><a class="pagination-link" aria-label="Goto page 4">4</a></li>
          <li><a class="pagination-link" aria-label="Goto page 5">5</a></li>
          <li><a class="pagination-link" aria-label="Goto page 6">6</a></li>
          <li><span class="pagination-ellipsis">&hellip;</span></li>
        </ul>
      </nav>
    </div>
  </div>
</template>

<script>
import axios from "axios";
import Pokemon from "./components/Pokemon";
export default {
  name: "App",
  data() {
    return {
      pokemons: []
    }
  },
  created: function () {
    axios
      .get("https://pokeapi.co/api/v2/pokemon?offset=1&limit=98&offset=0")
      .then(res => {
        console.log("Catch Pokemon list");
        this.pokemons = res.data.results;
      })
  },
  components: {
    Pokemon,
  },
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}
.Sel {
  margin-left: 50%;
  margin-bottom: 5%;
  font-weight: bolder;
}
.pesquisar {
  width: 30%;
  margin-left: 15%;
  margin-top: 30px;
  margin-bottom: -90px;
}
.nav{
  margin: 10px;
}
</style>
