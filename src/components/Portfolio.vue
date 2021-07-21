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
  <tfoot>
  <tr>
    <th>Total</th>
    <th></th>
    <th></th>
    <th></th>
    <th><Fund :portfolio="portfolio" :fund="fund" display="value" /></th>
    <th></th>
  </tr>
  </tfoot>
<tbody>
  <tr v-for="fund in funds">
    <td>
      {{ fund.name }}
    </td>
    <td>{{ fund.target }}</td>
    <td><Fund :portfolio="portfolio" :fund="fund" :target="fund.target" display="value" /></td>
    <td><Fund :portfolio="portfolio" :fund="fund" display="percent" /></td>
    <td><Fund :portfolio="portfolio" :fund="fund" display="value" /></td>
    <td><Fund :portfolio="portfolio" :fund="fund" :target="fund.target" display="diff" /></td>
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
    <th><Account :portfolio="portfolio" currency="ETH" :precision="4" /></th>
    <th><Account :portfolio="portfolio" currency="USD" /></th>
    <th><Account :portfolio="portfolio" currency="USDC" /></th>
    <th><Account :portfolio="portfolio" currency="Other" /></th>
    <th><Account :portfolio="portfolio" /></th>
  </tr>
  </tfoot>
<tbody>
  <tr v-for="account in portfolio.accounts">
    <td>
      {{ account.name }}
    </td>
    <td><Account :account="account" currency="ETH" :precision="4" /></td>
    <td><Account :account="account" currency="USD" /></td>
    <td><Account :account="account" currency="USDC" /></td>
    <td><Account :account="account" currency="Other" /></td>
    <td><Account :account="account" /></td>
  </tr>
</tbody>
</table>
</template>

<script>
import portfolio from '../../data/portfolio.json';
import Fund from './Fund.vue'
import Account from './Account.vue'

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


export default {
  name: 'Portfolio',
  components: {
    Account,
    Fund
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
