<template>
  <div class="container calculator">
    <form @submit.prevent="convert">
      <div class="form-group row" v-for="(field, index) in fieldList" :key="index">
        <label for="amount" class="col-sm-2 col-form-label">{{ field.label }}</label>

        <div class="col-sm-10">
          <input v-if="field.isTypeText" type="number" step="0.01" min="0" class="form-control" id="amount" placeholder="Amount" v-model="amount" />

          <select-field v-if="!field.isTypeText" :field="field" @selected-currency="calculateSelectedCurrency"></select-field>
        </div>
      </div>

      <button type="submit" class="btn btn-primary">Calculate</button>
      <button type="button" @click="clearResult" class="btn btn-danger">Clear</button>
    </form>
  </div>
</template>

<script>
import SelectField from './UI/SelectField.vue';

export default {
  inject: ['currencyList'],
  components: {
    SelectField,
  },
  data() {
    return {
      conversionFrom: '',
      conversionFromSymbol: '',
      conversionTo: '',
      conversionToSymbol: '',
      amount: 0,
      fieldList: [
        {
          label: 'Amount',
          isTypeText: true,
        },
        {
          label: 'From',
          isTypeText: false,

        },
        {
          label: 'To',
          isTypeText: false,
        },
      ],
    };
  },
  methods: {
    calculateSelectedCurrency(fieldData) {
      const [conversionType, conversionLabel] = fieldData;

      if (conversionType === this.fieldList[1].label) {
        this.conversionFrom       = conversionLabel.split('-')[0].trim();
        this.conversionFromSymbol = conversionLabel.split('-')[1].trim();
      }

      if (conversionType === this.fieldList[2].label) {
        this.conversionTo       = conversionLabel.split('-')[0].trim();
        this.conversionToSymbol = conversionLabel.split('-')[1].trim();
      }
    },
    convert() {

      if (!this.amount) {
        alert('Please enter a valid amount to convert.');
        return;
      }

      if (!this.conversionFrom) {
        alert('Please select a currency to convert from.');
        return;
      }

      if (!this.conversionTo) {
        alert('Please select a currency to convert to.');
        return;
      }

      let isResultToDisplay  = false;
      let fromCurrency       = this.currencyList.find(currency => currency.name === this.conversionFrom);

      let rate = 1;
      if (this.conversionFrom !== this.conversionTo) {
        let equivalent = fromCurrency.equivalents.find(equivalent => equivalent.name === this.conversionTo);
        rate           = equivalent.rate;
      }

      let convertedValue     = (this.amount * rate).toFixed(2);
      let message            = `
        ${this.amount} ${fromCurrency.name} (${this.conversionFromSymbol}) is ${convertedValue} ${this.conversionTo} (${this.conversionToSymbol})
      `;
      let calculatorData     = {
        isResultToDisplay: !isResultToDisplay,
        content: message,
      };

      this.$emit('display-result', calculatorData);
    },
    clearResult() {
      this.$emit('clear-result');
    },
  },
};
</script>

<style scoped>
form {
  width: 600px;
  text-align: center;
}

.calculator {
  margin: 100px auto;
  background-color: rgba(255, 208, 120, 0.5);
  display: flex;
  align-self: center;
  align-items: center;
  justify-content: center;
  max-width: 650px;
  padding: 15px;
}

button {
  margin: 15px 15px 0 0;
}
</style>
