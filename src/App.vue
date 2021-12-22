<template>
  <div id="app">
    <div v-if="!valuteflag">{{ getData() }}</div>
    <PageTable
        v-if="page===1"
        v-bind:valute="valute"
        v-bind:date="date"
        v-on:changePage1="page=2"
    />
    <PageConverter
        v-if="page===2"
        v-bind:valute="valute"
        v-bind:countries="countries"
        v-on:changePage2="page=1"
    />
  </div>
</template>

<script>

import PageTable from "./components/PageTable";
import PageConverter from "./components/PageConverter";

export default {
  name: 'App',
  data() {
    return {
      url: "https://www.cbr-xml-daily.ru/daily_json.js",
      valute: [{previous: [""]}],
      countries: ['RUB'],
      selected: ['RUB', 'USD'],
      date: "",
      valuteflag: false,
      page: 1,
      inputed1: "",
      outputed: "",
      selectedval1: 'RUB',
      selectedval2: 'USD',
    }
  },
  methods:
      {
        getData: function () {
          axios.get(this.url).then(response => {
            this.valute = response.data.Valute;
            this.date = response.data.Timestamp;
            this.valuteflag = true;
            for (let val in this.valute) {
              this.countries.push(val);
              this.valute[val].NumCode = Math.floor((this.valute[val].Value - this.valute[val].Previous) * 100) / 100;
            }
          });

        }
      },
  components: {PageConverter, PageTable}
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
