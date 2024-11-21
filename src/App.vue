<template>
  <header-nav></header-nav>
  <calculator
  @display-result="displayResult"
  @clear-result="clearResult"
  ></calculator>

  <result-display v-if="mustDisplayMessage" :message="resultMessage"></result-display>
</template>

<script>
import { currencyList } from '@/data/CurrencyList.js';
import HeaderNav from './components/UI/HeaderNav.vue';
import Calculator from './components/Calculator.vue';
import ResultDisplay from './components/UI/ResultDisplay.vue';

export default {
  components: {
    Calculator,
    HeaderNav,
    ResultDisplay,
  },
  data() {
    return {
      currencyList: currencyList,
      resultMessage: '',
      mustDisplayMessage: false,
    };
  },
  provide() {
    return {
      currencyList: this.currencyList,
    };
  },
  methods: {
    displayResult(message) {
      this.mustDisplayMessage = message.isResultToDisplay;
      this.resultMessage      = message.content;
    },
    clearResult() {
      this.mustDisplayMessage = false;
    },
  },
  // mounted() {
  // Latest rates
  // ?symbols=EUR,USD,GBP,RUB
  // fetch('https://api.frankfurter.app/latest')
  // .then(response => response.json())
  // .then(data => {
    // console.log(data);
    // if ('rates' in data) {
      // let rateList = data.rates;
      // console.log('rateList', rateList);
      // for (let index in rateList) {
      //   console.log(rateList[]);
      // }
    // }
  // })
  // .catch(error => console.error('Error:', error));
  // },
};
// https://www.oanda.com/currency-converter/en/?from=EUR&to=RUB&amount=1

</script>

<style>
body {
  margin: 0;
  padding: 0;
  background-image: url("images/main_background.jpg");
  background-repeat: no-repeat;
  background-size: contain;
  background-position: left top;
  background-repeat: no-repeat;
  background-attachment: fixed;
  font-size: larger;
  font-weight: bolder;
  min-height: 100vh;
}

.form--calculator {
  width: 50%;
}

#value1,
#value2 {
  display: inline-block;
  margin: 1px;
}

.form--input--area {
  display: flex;
  align-items: center;
  justify-content: center;
}

.input-request {
  display: inline-block;
  margin: 2px;
}

.resultMessage {
  color: blue;
}
</style>
