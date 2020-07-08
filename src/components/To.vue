<template lang="pug">
  .row
    .col
      b-form-input(v-if="amountTo" id="amountTo" type="number" v-model="amountTo.toFixed(4)" disabled)
      b-form-input(v-else id="amountTo" type="number" disabled)
    .col
      b-form-select(v-model="selectedTo" :options="options")
</template>
<script>
export default {
  props: {
    rates: Object,
    options: Array,
    amountFrom: Number
  },
  data() {
    return {
      selectedTo: "CAN"
    };
  },
  computed: {
    amountTo() {
      return this.rates ? this.rates[this.selectedTo] * this.amountFrom : null;
    }
  },
};
</script>