<template>
    <div class="calculator container">
      <form class="form--calculator" submit.prevent="">
        <div class="mb-3" v-for="(field, index) in fieldList" :key=" index">
          <form-field :label="field.label" :hasTextInput="field.hasTextInput"></form-field>
        </div>

        <div class="mb-3">
          <button class="btn btn-primary">Calculate</button>
        </div>

        <div class="resultMessage" v-if="false">Result</div>
      </form>
  </div>
</template>

<script>
import FormField from './FormField.vue';

export default {
  components: {
    FormField,
  },
  data() {
    return {
      fieldList: [
        {
          label: 'Amount',
          hasTextInput: true,
        },
        {
          label: 'Convert from',
          hasTextInput: false,
        },
        {
          label: 'Convert to',
          hasTextInput: false,
        },
      ],
    };
  },  
};
</script>
