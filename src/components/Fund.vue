<template>
{{ value() }}
</template>

<script>
import Holding from '../mixins/Holding.vue';

export default {
  name: 'Fund',
  mixins: [Holding],
  props: {
    fund: Object,
    target: Number
  },
  methods: {
    value() {
        var total = 0;

        if (this.fund != null) {
          // Display total for fund
          var grandTotal = 0;
          for(var i = 0; i < this.portfolio.accounts.length; i++) {
            var account = this.portfolio.accounts[i];
            for(var j = 0; j < account.holdings.length; j++) {
              var holding = account.holdings[j];
              var accountFund = holding.fund;
              if (accountFund == this.fund.name) {
                total += holding.value;
              }
              grandTotal += holding.value;
            }
          }

          if (this.target != null) {
            if (this.display == "diff") {
              // Display the difference between actual value and the target
              total = (grandTotal * this.target) - total;
            } else {
              // Display target $ for this fund
              total = grandTotal * this.target;
            }
          } else if (this.display == "percent") {
            // Display what % of the total this fund contains
            total = total / grandTotal * 100;
          }
        } else {
          // Display total for portfolio
          total = this.getPortfolioTotal();
        }

        return this.getLocaleString(total);
    }
  }
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
</style>
