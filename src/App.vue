<template>
  <div id="nav">
    <router-link to="/">Home</router-link> |
    <router-link to="/job">Job</router-link>
  </div>
  <router-view />
</template>

<script lang="ts">
import { defineComponent } from 'vue';

export default defineComponent({
  name: 'App',
});
</script>

<style lang="scss" src="./styles/index.scss"></style>
