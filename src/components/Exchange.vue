<template lang="pug">
  .container
    .card.m-4
      .card-header Exchange Rate
      .card-body.p-4
        .row.p-4
          .col-5.p-4 1
            b-form-select(v-model="selectedFrom" :options="options" @change="getRates")
          .col-2.p-4
            h1 =
          .col-5.p-4
            div(v-if="rate") {{rate.toFixed(4)}}
            b-form-select(v-model="selectedTo" :options="options")
            //- .row(v-for="(rate, currency) in rates" :key="currency")
            //-   .col
            //-     | {{currency}}: {{rate}}
</template>

<script>
import axios from "axios";
export default {
  data() {
    return {
      rates: null,
      selectedFrom: "CAD",
      selectedTo: "CAD",
      error: null,
      options: [
        "CAD",
        "HKD",
        "ISK",
        "PHP",
        "DKK",
        "HUF",
        "CZK",
        "GBP",
        "RON",
        "SEK",
        "IDR",
        "INR",
        "BRL",
        "RUB",
        "HRK",
        "JPY",
        "THB",
        "CHF",
        "EUR",
        "MYR",
        "BGN",
        "TRY",
        "CNY",
        "NOK",
        "NZD",
        "ZAR",
        "USD",
        "MXN",
        "SGD",
        "AUD",
        "ILS",
        "KRW",
        "PLN"
      ]
    };
  },
  mounted() {
    this.getRates();
  },
  methods: {
    async getRates() {
      await axios
        .get(`https://api.exchangeratesapi.io/latest?base=${this.selectedFrom}`)
        .then(response => {
          // console.log(response.data);
          this.rates = response.data.rates;
          // console.log(this.rates);
        })
        .catch(error => {
          this.error = error;
          console.warn("Failed to fetch rates");
        });
    }
  },
  computed: {
    rate() {
      return this.rates ? this.rates[this.selectedTo] : null;
    }
  }
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
</style>
