<template>
  <div class="calculator-field">
    <label htmlFor="value">{{ label }} </label>

    <input v-if="hasTextInput"
      id="value"
      name="value"
      class="form-control input-request"
      type="text"
      placeholder="Enter value"
      required
    />

    <div v-if="!hasTextInput" class="">
      <select class="form-select" @change="selectCurrency">
        <option v-for="(currency, index) in currencyList" :key="index">
          {{ currency.name + ' ' + currency.symbol }}
        </option>
      </select>
    </div>
  </div>
</template>

<script>
export default {
  inject: ['currencyList'],
  props: ['label', 'hasTextInput'],
  data() {},
  methods: {
    selectCurrency(event) {
      console.log(event.target.value);
    },
  },
};
</script>

<style scoped>
.calculator-field {
  display: flex;
  align-items: center;
  justify-content: space-between;
}
</style>
