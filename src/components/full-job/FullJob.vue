<template>
  <div class="wrapper">
    <h1>{{ job.title }}</h1>
    <p v-html="job.description" />
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
  width: 500px;
  height: 200px;
  display: flex;
}

.img-wrapper {
  position: relative;
  width: 150px;
  height: 150px;
}

.img {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  object-fit: cover;
}
</style>
