<template>
{{ value().toLocaleString() }}
</template>

<script>

function getHoldingTotal(holding, currency, display) {
  var total = 0;
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
}

export default {
  name: 'Holding',
  props: {
    account: Object,
    portfolio: Object,
    currency: String,
    precision: {
      type: Number,
      default:2
    },
    display: String
  },
  methods: {
    value() {
        var total = 0;
        if (this.portfolio != null) {
          // Display total for portfolio
          for(var i = 0; i < this.portfolio.accounts.length; i++) {
            var account = this.portfolio.accounts[i];
            for(var j = 0; j < account.holdings.length; j++) {
             var holding = account.holdings[j];
             total += getHoldingTotal(holding, this.currency, this.display)
            }
          }
        } else if (this.account != null) {
          // Display total for single account
          for(var i = 0; i < this.account.holdings.length; i++) {
            var holding = this.account.holdings[i];
            total += getHoldingTotal(holding, this.currency, this.display)
          }
        }
        const options = { 
          minimumFractionDigits: 2,
          maximumFractionDigits: this.precision
        };

        return total.toLocaleString('en', options);
    }
  }
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
</style>
