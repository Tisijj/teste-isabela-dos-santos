<template>
  <div id="app">
    <b-card id="container">
      <h1>COVID 19 - API</h1>
      <h3 style="color: #bdbdbd">Informações do COVID por Estado Brasileiro</h3>
      <div>
        <b-form-select
          v-model="valorUf"
          :options="opcoesUf"
          style="max-width: 30rem"
          size="sm"
          class="mt-3"
        ></b-form-select>
      </div>

      <div class="botoesDeAcao">
        <b-button v-on:click="getCovidPorEstado">Procurar Casos</b-button>
        <b-button v-on:click="limparResultados">Limpar Resultados</b-button>
      </div>

      <div v-if="Object.keys(casosPorEstado).length > 0" class="cardContainer">
        <b-card
          :title="casosPorEstado.state"
          tag="article"
          style="max-width: 25rem; padding: 15px"
          class="mb-2"
        >
          <b-card-text>Casos: {{ casosPorEstado.cases }}</b-card-text>
          <b-card-text>Suspeitas: {{ casosPorEstado.suspects }}</b-card-text>
          <b-card-text>Mortes: {{ casosPorEstado.deaths }}</b-card-text>
        </b-card>
      </div>
    </b-card>
  </div>
</template>

<script>
export default {
  name: "App",
  components: {},
  data() {
    return {
      baseUrl: "https://covid19-brazil-api.now.sh/api/report/v1",
      casosPorEstado: {},
      opcoesUf: [
        { value: null, text: "Selecione um Estado" },
        { value: "AC", text: "Acre" },
        { value: "AL", text: "Alagoas" },
        { value: "AM", text: "Amazonas" },
        { value: "AP", text: "Amapá" },
        { value: "BA", text: "Bahia" },
        { value: "CE", text: "Ceará" },
        { value: "DF", text: "Distrito Federal" },
        { value: "ES", text: "Espírito Santo" },
        { value: "GO", text: "Goiás" },
        { value: "MA", text: "Maranhão" },
        { value: "MT", text: "Mato Grosso" },
        { value: "MS", text: "Mato Grosso do Sul" },
        { value: "MG", text: "Minas Gerais" },
        { value: "PA", text: "Pará" },
        { value: "PB", text: "Paraíba" },
        { value: "PR", text: "Paraná" },
        { value: "PE", text: "Pernambuco" },
        { value: "PI", text: "Piauí" },
        { value: "RJ", text: "Rio de Janeiro" },
        { value: "RN", text: "Rio Grande do Norte" },
        { value: "RO", text: "Rondônia" },
        { value: "RS", text: "Rio Grande do Sul" },
        { value: "RR", text: "Roraima" },
        { value: "SC", text: "Santa Catarina" },
        { value: "SE", text: "Sergipe" },
        { value: "SP", text: "São Paulo" },
        { value: "TO", text: "Tocantis" },
      ],
      valorUf: null,
    };
  },
  mounted() {},
  methods: {
    getCovidPorEstado: function () {
      fetch(`${this.baseUrl}/brazil/uf/${this.valorUf}`, {
        method: "GET",
      })
        .then((res) => res.json())
        .then((data) => (this.casosPorEstado = data))
        .catch((err) => console.error(err));
    },

    limparResultados: function () {
      this.casosPorEstado = {};
      this.valorUf = null;
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

#container {
  width: 85%;
  margin: auto;
}

.botoesDeAcao {
  display: flex;
  justify-content: center;
  margin: 20px 0px;
  :last-child {
    margin-left: 20px;
  }
}

.cardContainer {
  display: flex;
  justify-content: center;
}

.card-title {
  font-size: 2rem !important;
}
</style>
