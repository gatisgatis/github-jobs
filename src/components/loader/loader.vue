<template>
  <div class="loader" />
</template>

<script lang="ts">
import { defineComponent } from 'vue';

export default defineComponent({});
</script>

<style scoped lang="scss">
.loader {
  border: 25px solid #f3f3f3; /* Light grey */
  border-top: 25px solid #3498db; /* Blue */
  border-radius: 50%;
  width: 60%;
  padding-top: 60%;
  animation: spin 2s linear infinite;
}

@keyframes spin {
  0% {
    transform: rotate(0deg);
  }
  100% {
    transform: rotate(360deg);
  }
}
</style>
