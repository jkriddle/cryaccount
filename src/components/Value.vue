<template>
{{ value() }}
</template>

<script>
export default {
  name: 'Value',
  props: {
    account: Object,
    currency: String
  },
  methods: {
    value() {
        var total = 0;
        for(var i = 0; i < this.account.holdings.length; i++) {
          var holding = this.account.holdings[i];
          if (holding.currency == this.currency) {
            total += holding.value;
          }
        }
        return total;
    }
  }
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
</style>
