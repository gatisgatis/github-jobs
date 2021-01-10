<template>
  <div class="wrapper">
    <router-link class="link-to-home" :to="'/'">Back To Search</router-link>
    <div class="title">TO APPLY</div>
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
*{
  color:#334680;
}
.wrapper {
  padding: 10px;
}

.link-to-home {
  color: blue;
  font-weight: bold;
  cursor: pointer;
  margin-bottom: 20px;
}

.title {
  color: #B9BDCF;
  margin: 20px 0;
  font-weight: 900;
}
</style>
