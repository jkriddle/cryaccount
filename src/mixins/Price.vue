<template>
</template>

<script>

export default {
  name: 'Price',
  methods: {
    getPrice(symbol) {
      if (symbol == 'ETH') return 1900;
      if (symbol == 'USDC') return 1;
      if (symbol == 'USD') return 1;
      if (symbol == 'Other') return 1;
    }
  }
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
</style>
