<template>
  <div class="hwotodasdas">
    <router-link :to="'/'">Back To Search</router-link>
    <h2>HOW TO APPLY</h2>
    <p v-html="howToApply" />
  </div>
</template>

<script lang="ts">
import { defineComponent } from 'vue';

export default defineComponent({
  props: {
    howToApply: {
      type: String,
      required: true,
    },
  },
  computed: {},
});
</script>

<style scoped lang="scss">
.hwotodasdas {
  background-color: orange;
}
</style>
