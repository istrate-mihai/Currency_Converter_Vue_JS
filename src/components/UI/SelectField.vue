<template>
  <div class="form-group">
    <select class="form-select" aria-label="Default select example" @change="selectCurrency" v-model="selectedCurrency">
      <option :class="field.label" v-for="(currency, index) in currencyList" :key="index">{{ currency.name + ' - ' + currency.symbol }}</option>
    </select>
  </div>
</template>

<script>
export default {
  inject: ['currencyList'],
  props: {
    field: {
      label: String,
      isTypeText: Boolean,
    },
  },
  data() {
    return {
      selectedCurrency: '',
    } 
  },
  methods: {
    selectCurrency() {
      let fieldData = [this.field.label, this.selectedCurrency]
      this.$emit('selected-currency', fieldData);
    },
  },
}
</script>
