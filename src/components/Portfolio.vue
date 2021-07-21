<template>
<h3>Funds</h3>

<table class="table table-bordered table-hover">
  <thead>
    <tr>
      <th scope="col">Fund</th>
      <th class="text-end" scope="col">Target %</th>
      <th class="text-end" scope="col">Target $</th>
      <th class="text-end" scope="col">Actual %</th>
      <th class="text-end" scope="col">Actual $</th>
      <th  class="text-end"scope="col">Diff $</th>
    </tr>
  </thead>
  <tfoot>
  <tr>
    <th scope="col">Total</th>
    <th class="text-end" scope="col"></th>
    <th class="text-end" scope="col"></th>
    <th class="text-end" scope="col"></th>
    <th class="text-end" scope="col">
      <Fund :portfolio="portfolio" :fund="fund" display="value" />
    </th>
    <th class="text-end" scope="col"></th>
  </tr>
  </tfoot>
<tbody>
  <tr v-for="fund in funds">
    <td>
      {{ fund.name }}
    </td>
    <td class="text-end">
      {{ fund.target }}
    </td>
    <td class="text-end">
      <Fund :portfolio="portfolio" :fund="fund" :target="fund.target" display="value" />
    </td>
    <td class="text-end">
      <Fund :portfolio="portfolio" :fund="fund" display="percent" />
    </td>
    <td class="text-end">
      <Fund :portfolio="portfolio" :fund="fund" display="value" />
    </td>
    <td class="text-end">
      <Fund :portfolio="portfolio" :fund="fund" :target="fund.target" display="diff" />
    </td>
  </tr>
</tbody>
</table>


<h3>Accounts</h3>
  
<table class="table table-bordered table-hover table-responsive">
  <thead>
    <tr>
      <th scope="col">Account</th>
      <th class="text-end" scope="col">ETH</th>
      <th class="text-end" scope="col">USD</th>
      <th class="text-end" scope="col">USDC</th>
      <th class="text-end" scope="col">Value (Other)</th>
      <th class="text-end" scope="col">Total</th>
      <th>Comment</th>
    </tr>
  </thead>
  <tfoot>
    <tr>
      <th scope="col">Total</th>
      <th class="text-end" scope="col"><Account :portfolio="portfolio" currency="ETH" :precision="4" /></th>
      <th class="text-end" scope="col"><Account :portfolio="portfolio" currency="USD" /></th>
      <th class="text-end" scope="col"><Account :portfolio="portfolio" currency="USDC" /></th>
      <th class="text-end" scope="col"><Account :portfolio="portfolio" currency="Other" /></th>
      <th class="text-end" scope="col"><Account :portfolio="portfolio" /></th>
      <th></th>
    </tr>
  </tfoot>
<tbody>
  <tr v-for="account in portfolio.accounts">
    <td>
      {{ account.name }}
    </td>
    <td class="text-end"><Account :account="account" currency="ETH" :precision="4" /></td>
    <td class="text-end"><Account :account="account" currency="USD" /></td>
    <td class="text-end"><Account :account="account" currency="USDC" /></td>
    <td class="text-end"><Account :account="account" currency="Other" /></td>
    <th class="text-end" scope="row"><Account :account="account" /></th>
    <td class="fst-italic">{{ account.comment }}</td>
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
