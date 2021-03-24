<template>
  <div class="container">
    <div class="card">
      <div class="Fundo card-image">
        <figure class="Imgp image is-4by3">
          <img :src="pokemon.front" alt="Pokemon" />
        </figure>
      </div>
      <div class="card-content">
        <div class="media">
          <div class="media-content">
            <p class="Num subtitle is-6">Nº {{ num }}</p>
            <p class="title is-4">{{ name | upper }}</p>

            <p style="margin-top: 1rem" class="subtitle is-6">
              <span
                style="
                  padding: 0.5rem 1rem;
                  background-color: red;
                  color: #fff;
                  margin-right: 0.5rem;
                  border-radius: 0.5rem;
                "
              >
                {{ pokemon.type | upper }}
              </span>

              <span
                class="b2"
                style="
                  padding: 0.5rem 1rem;
                  background-color: #4592c4;
                  color: #fff;
                  border-radius: 0.5rem;
                "
              >
                {{ pokemon.type == "" ? " " : pokemon.type | upper }}
              </span>
            </p>
            <!--<p class="subtitle is-6">{{ pokemon.type[1] != ""? pokemon.type[1]: "null" | upper }}</p>-->
          </div>
        </div>
        <div class="content">
          <button
            class="button is-info is-large is-fullwidth is-light"
            @click="exibirDescricaoTeste"
          >
            Detalhes
          </button>
        </div>
        <div>
          <footer class="card-footer">
    <a href="#" class="card-footer-item">Inserir</a>
    <a href="#" class="card-footer-item">Editar</a>
    <a href="#" class="card-footer-item">Deletar</a>
  </footer>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import axios from "axios";

export default {
  created: function () {
    axios.get(this.url).then((res) => {
      this.pokemon.type = res.data.types[0].type.name;
      this.pokemon.front = res.data.sprites.front_default;
      this.pokemon.back = res.data.sprites.back_default;
      this.pokemon.description = res.data.description_default;
      this.currentImg = this.pokemon.front;
      console.log(this.pokemon);
    });
  },

  data() {
    return {
      ifFront: true,
      currentImg: "",
      pokemon: {
        type: "",
        front: "",
        back: "",
        description: "",
      },
    };
  },

  props: {
    num: Number,
    name: String,
    url: String,
  },
  filters: {
    upper: function (value) {
      var newName = value[0].toUpperCase() + value.slice(1);
      return newName;
    },
  },

  methods: {
    exibirDescricaoTeste: function () {
      document.write("Modal");
    },

    mudarSprite: function () {
      if (this.isFront) {
        this.isFront = false;
        this.currentImg = this.pokemon.back;
      } else {
        this.isFront = true;
        this.currentImg = this.pokemon.front;
      }
    },
  },
};
</script>

<style>
.container {
  font-family: "Times New Roman", Times, serif;
}
.Num {
  color: #919191;
}
.card {
  border-radius: 10px;
  border: 1px solid red;
}
.card:hover {
  -webkit-box-shadow: 0px 0px 15px -7px rgba(0, 0, 0, 0.82);
  -moz-box-shadow: 0px 0px 15px -7px rgba(0, 0, 0, 0.82);
  box-shadow: 0px 0px 15px -7px rgba(0, 0, 0, 0.82);
  -webkit-transform: translateX(-3px);
  transform: translateX(-3px);
  border-radius: 10px;
}
.Fundo {
  background-color: #f2f2f2;
  border-radius: 10px;
}
</style>
