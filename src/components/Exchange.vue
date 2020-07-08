<template lang="pug">
  .container
    Loading(:active.sync="isLoading"
      is-full-page=true)
    .card.m-4.border-0.shadow-lg.rounded
      .card-header.bg-success
        h2 Currency Exchange
      .card-title.p-2.bg-danger(v-if="error")
        .text-center.text-white
          h4 {{error}}
      .card-body.p-4
        .row.p-4
          .col-5.p-4
            .row
              .col
                b-form-input(id="amountFrom" type="number" v-model="amountFrom")
              .col
                b-form-select(v-model="selectedFrom" :options="options" @change="getRates")
          .col-2.p-4
            h1 =
          .col-5.p-4
            .row
              .col
                b-form-input(v-if="amountTo" id="amountTo" type="number" v-model="amountTo.toFixed(4)" disabled)
              .col
                b-form-select(v-model="selectedTo" :options="options")
            //- .row(v-for="(rate, currency) in rates" :key="currency")
            //-   .col
            //-     | {{currency}}: {{rate}}
</template>

<script>
import axios from "axios";
import Loading from "vue-loading-overlay";
import "vue-loading-overlay/dist/vue-loading.css";
export default {
  components: {
    Loading
  },
  data() {
    return {
      isLoading: true,
      amountFrom: 1,
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

  async created() {
    try {
      let res = await fetch(
        `https://source.unsplash.com/1600x900/?money`
      ).catch();
      document.body.style.backgroundImage = (await "url('") + res.url + "')";
    } catch (err) {
      console.log("Failed to load random remote image,", err);
    }
  },
  methods: {
    async getRates() {
      this.isLoading = true;
      await axios
        .get(`https://api.exchangeratesapi.io/latest?base=${this.selectedFrom}`)
        .then(response => {
          this.rates = response.data.rates;
        })
        .catch(error => {
          this.error = "Failed to fetch rates";
          console.warn("Failed to fetch rates", error);
        })
        .finally(() => {
          this.isLoading = false;
        });
    }
  },
  computed: {
    amountTo() {
      return this.rates ? this.rates[this.selectedTo] * this.amountFrom : null;
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
