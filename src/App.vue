<template>
  <calculator :currencyList="currencyList"></calculator>
</template>

<script>
import { currencyList } from '@/data/CurrencyList.js';
import Calculator from './components/Calculator.vue';

export default {
  components: {
    Calculator,
  },
  data() {
    return {
      currencyList: currencyList, 
    };
  },
  provide() {
    return {
      currencyList: this.currencyList,
    };
  },
};
</script>

<style>
body {
  padding: 0;
  margin: 0;
  font-size: larger;
  font-weight: bolder;
  background-image: url("images/main_background.jpg");
  background-repeat: no-repeat;
  background-size: contain;
}

.calculator {
  margin: 100px auto;
  width: 80%;
  text-align: center;
  padding: 2px;
  background-color: rgba(255, 208, 120, 0.5);
  display: flex;
  align-self: center;
  align-items: center;
  justify-content: center;
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
