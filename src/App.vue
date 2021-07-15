<template>
  <div id="app">
    <div>
      <b-button v-on:click="buscaCep">Buscar dados rua</b-button>
      <h1>{{ dadosRua }}</h1>
    </div>
    <div>
      <b-button v-on:click="listaCasosEstado">Buscar Casos por Estado</b-button>
      <h1>{{ covidPorEstado }}</h1>
    </div>
  </div>
</template>

<script>
export default {
  name: "App",
  components: {},
  data() {
    return {
      dadosRua: [],
      covidPorEstado: [],
    };
  },
  mounted() {},
  methods: {
    buscaCep: function () {
      const baseUrl = "https://brasilapi.com.br/api";
      fetch(`${baseUrl}/cep/v2/cep=37500208`)
        .then((res) => res.json())
        .then((data) => (this.dadosRua = data))
        .catch((err) => console.log(err.message));
    },
    listaCasosEstado: function () {
      const baseUrl = "https://covid19-brazil-api.now.sh/api/report/v1";
      fetch(`${baseUrl}/brazil/uf/sp`)
        .then((res) => res.json())
        .then((data) => (this.covidPorEstado = data))
        .catch((err) => console.log(err.message));
    },
  },
};
</script>

<style lang="scss">
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
