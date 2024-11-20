<template>
  <div class="container card">
    <div class="card-body">
      {{ message }}
    </div>
  </div>
</template>

<script>
export default {
  props: ['message'],
}
</script>

<style scoped>
.card {
  background-color: rgba(255, 208, 120, 0.5);
  max-width: 650px;
}
</style>
