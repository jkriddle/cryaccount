<template>
<h3>Funds</h3>
<table>
  <thead>
    <tr>
      <th>Fund</th>
      <th>Target %</th>
      <th>Target $</th>
      <th>Actual %</th>
      <th>Actual $</th>
      <th>Diff $</th>
    </tr>
  </thead>
<tbody>
  <tr v-for="fund in funds">
    <td>
      {{ fund.name }}
    </td>
    <td></td>
    <td></td>
    <td></td>
    <td>{{fund.value}}</td>
    <td></td>
  </tr>
</tbody>
</table>


  <h3>Accounts</h3>
  
<table>
  <thead>
    <tr>
      <th>Wallet/Exchange</th>
      <th>ETH</th>
      <th>USD</th>
      <th>USDC</th>
      <th>Value (Other)</th>
      <th>Total</th>
    </tr>
  </thead>
<tbody>
  <tr v-for="account in portfolio.accounts">
    <td>
      {{ account.name }}
    </td>
    <td><Value :account="account" currency="ETH" /></td>
    <td><Value :account="account" currency="USD" /></td>
    <td><Value :account="account" currency="USDC" /></td>
    <td><Value :account="account" currency="Other" /></td>
    <td>{{account.value}}</td>
  </tr>
</tbody>
</table>
</template>

<script>
import portfolio from '../../data/portfolio.json';

var funds = portfolio.funds;

for(var i = 0; i < portfolio.accounts.length; i++) {
  var account = portfolio.accounts[i];
  for(var j = 0; j < account.holdings.length; j++) {
    var holding = account.holdings[j];
    var accountFund = holding.fund;

    for(var k = 0; k < portfolio.funds.length; k++) {
      var fund = portfolio.funds[k];
      if (fund.name == accountFund) {
        fund.value += holding.value;
      }
    }
   
  }
}

import Value from './Value.vue'

export default {
  name: 'Portfolio',
  components: {
    Value
  },
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
