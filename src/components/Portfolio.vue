<template>
<h3>Funds</h3>
  <ul>
    <li v-for="fund in funds">
      {{ fund.name }} : ${{ fund.value }}
    </li>
  </ul>

  <h3>Accounts</h3>
  <ul>
    <li v-for="account in portfolio.accounts">
      {{ account.name }}
    </li>
  </ul>
</template>

<script>
import portfolio from '../../data/portfolio.json';

var funds = {};
for(var i = 0; i < portfolio.accounts.length; i++) {
  var account = portfolio.accounts[i];
  for(var j = 0; j < account.holdings.length; j++) {
    var holding = account.holdings[j];
    var category = holding.category;
    if (funds[category] == null) {
      funds[category] = { name: category, amount: 0, value: 0};
    }
    funds[category].amount += holding.amount;
    funds[category].value += holding.value;
  }
}

export default {
  name: 'Portfolio',
  data() {
    return {
      // Initialized to zero to begin
      portfolio,
      funds
    }
  },
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
</style>
