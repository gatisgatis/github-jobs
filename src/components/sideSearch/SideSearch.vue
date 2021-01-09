<template>
  <div class="sideSearchComponent">
    <div class="checkboxWrapper">
      <input type="checkbox" id="checkbox" v-model="checkboxValue" @change="sendChekboxValue" />
      <label for="checkbox">Full Time</label>
    </div>
    <div class="inputWrapper">
      <input
        v-model="sideSearchValue"
        placeholder="City, state, zip code or country"
        @change="sendSideSearchValue"
        @keyup.enter="sideSearchEnterPress"
      />
    </div>
    <template v-for="(city, index) in cities" :key="index" >
      <input type="radio" :id="city" :value="city" v-model="pickedRadio" @change="sendRadioValue" />
      <label :for="city">{{city}}</label>
      <br />
    </template>
  </div>
</template>

<script lang="ts">
import { defineComponent } from 'vue';

export default defineComponent({
  data() {
    return {
      cities: ['London', 'Amsterdam', 'New York', 'Berlin'],
      checkboxValue: false,
      sideSearchValue: '',
      pickedRadio: '',
    };
  },
  methods: {
    sendSideSearchValue() {
      this.$emit('sideSearchValueUpdated', this.sideSearchValue);
    },
    sendChekboxValue() {
      this.$emit('checkboxValueUpdated', this.checkboxValue);
    },
    sendRadioValue() {
      this.$emit('radioValueUpdated', this.pickedRadio);
    },
    sideSearchEnterPress() {
      this.$emit('sideSearchEnterPressed');
    },
  },
});
</script>

<style scoped></style>
