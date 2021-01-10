<template>
  <div class="wrapper">
    <h1>{{ job.title }}</h1>
    <p v-html="job.description" />
    <h3>{{ job.how_to_apply }}</h3>
  </div>
</template>

<script lang="ts">
import { defineComponent } from 'vue';

export default defineComponent({
  props: {
    job: {
      type: Object,
      required: true,
    },
  },
  methods: {
    goToJobPage() {
      this.$router.push('/About');
    },
  },
});
</script>

<style scoped lang="scss">
.wrapper {
  border: 2px solid red;
  width: 100%;
}
</style>
