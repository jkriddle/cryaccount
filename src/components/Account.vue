<template>
{{ value() }}
</template>

<script>
import Holding from '../mixins/Holding.vue';

export default {
  name: 'Account',
  mixins: [Holding],
  props: {
    account: Object,
    currency: String
  },
  methods: {
    value() {
        var total = 0;

        if (this.portfolio != null) {
          // Display total for portfolio
          total = this.getPortfolioTotal();
        } else if (this.account != null) {
          // Display total for single account
          for(var i = 0; i < this.account.holdings.length; i++) {
            var holding = this.account.holdings[i];
            total += this.getHoldingTotal(holding, this.currency, this.display)
          }
        }

        return this.getLocaleString(total);
    }
  }
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
</style>
