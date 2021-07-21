<template>
</template>

<script>

export default {
  name: 'Holding',
  props: {
    portfolio: Object,
    target: Number,
    precision: {
      type: Number,
      default:2
    },
    display: String
  },
  methods: {
    getHoldingTotal(holding, currency, display) {
      var total : decimal = 0;
      if (currency == null || holding.currency == currency) {
        if (holding.currency == "ETH") {
          if (currency == null || display == "value") {
            total += holding.value;
          }
          else {
            total += holding.amount;
          }
        } else {
          total += holding.value;
        }
      }
      return total;
    },
    getPortfolioTotal() {
      var total : decimal = 0;
      for(var i = 0; i < this.portfolio.accounts.length; i++) {
        var account = this.portfolio.accounts[i];
        for(var j = 0; j < account.holdings.length; j++) {
          var holding = account.holdings[j];
          total += this.getHoldingTotal(holding, this.currency, this.display)
        }
      }
      return total;
    },
    getLocaleString(value, precision) {
      const localeOptions = { 
        minimumFractionDigits: 2,
        maximumFractionDigits: this.precision
      };

      var formatted = value.toLocaleString('en', localeOptions);

      // Replace negative symbol with parenthesis
      return value < 0 ? '(' + formatted.slice(1) + ')' : formatted;

    }
  }
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
</style>
