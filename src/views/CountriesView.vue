<script>
import countries from "/src/datasets/countries.json";
import CountryComponent from "../components/CountryComponent.vue";

export default {
  name: "CountriesView",
  components: {
    CountryComponent,
  },
  data() {
    return {
      countries: [],
      paisActual: "",
    };
  },
  created() {
    this.countries = countries;
  },
  methods: {
    filtrarPais(e) {
      // TODO: Implementar. filtra el país de acuerdo al valor del input. Hint: Recuerda la función filter
      const filtro = e.target.value;
      this.paisActual = filtro;
      this.countries = countries.filter((country) =>
        country.name.toLowerCase().includes(this.paisActual.toLowerCase())
      );
    },
  },
};
</script>

<template>
  <div class="countries">
    <input
      placeholder="Busca un país"
      :value="this.paisActual"
      @input="filtrarPais"
    />
  </div>
  <div class="countries-container">
    <!--//TODO: pasar una propiedad para determinar si al componente se le puede hacer click -->
    <CountryComponent
      v-for="(country, index) in countries"
      :key="index"
      :name="country.name"
      :capital="country.capital"
      :currency_name="country.currency_name"
      :currency="country.currency"
      :region="country.region"
      :code="country.iso2"
      :clickable="true"
    ></CountryComponent>
  </div>
</template>

<style scoped>
@media (min-width: 1024px) {
  .countries {
    display: flex;
    align-items: center;
  }

  input {
    line-height: 2em;
  }

  .countries-container {
    text-align: center;
    overflow-y: auto;
    vertical-align: middle;
    display: grid;
    grid-template-columns: auto auto auto;
    grid-gap: 10px;
    padding: 10px;
  }
}
</style>
