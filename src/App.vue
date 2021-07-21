<template>
  <div id="app">
    <Portfolio />
  </div>
</template>

<script>
import Portfolio from './components/Portfolio.vue';

export default {
  name: 'App',
  components: {
    Portfolio
  },
  data() {
    return {
      polling: null,
      prices: null
    }
  },
  beforeDestroy() {
    clearInterval(this.polling);
  },
  created() {
    this.pollData();
  },
  methods: {
    getPrice() {
      return 5;
    },
    pollData() {
      this.polling = setInterval(() => {
        //this.$store.dispatch('RETRIEVE_DATA_FROM_BACKEND');
        fetch('https://api.coingecko.com/api/v3/simple/price?ids=ethereum&vs_currencies=usd&include_24hr_change=true')
        .then(r => r.json())
        .then((data) => {
          this.prices = data;
          console.log('data update');
        });
      }, 10000);
    }
  }
}
</script>

<style>
#app {
  margin:20px;
}
</style>
