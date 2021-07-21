<template>
<h3>Funds</h3>

<table class="table table-sm table-bordered">
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
    <td><Holding :portfolio="portfolio" :fund="fund" /></td>
    <td></td>
  </tr>
</tbody>
</table>


  <h3>Accounts</h3>
  
<table class="table table-sm table-bordered">
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
  <tfoot>
  <tr>
    <th>Total</th>
    <th><Holding :portfolio="portfolio" currency="ETH" :precision="4" /></th>
    <th><Holding :portfolio="portfolio" currency="USD" /></th>
    <th><Holding :portfolio="portfolio" currency="USDC" /></th>
    <th><Holding :portfolio="portfolio" currency="Other" /></th>
    <th><Holding :portfolio="portfolio" /></th>
  </tr>
  </tfoot>
<tbody>
  <tr v-for="account in portfolio.accounts">
    <td>
      {{ account.name }}
    </td>
    <td><Holding :account="account" currency="ETH" :precision="4" /></td>
    <td><Holding :account="account" currency="USD" /></td>
    <td><Holding :account="account" currency="USDC" /></td>
    <td><Holding :account="account" currency="Other" /></td>
    <td><Holding :account="account" /></td>
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

import Holding from './Holding.vue'

export default {
  name: 'Portfolio',
  components: {
    Holding
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
