<template>
  <div class="sideSearchComponent">
    <div class="checkboxWrapper">
      <input type="checkbox" id="checkbox" v-model="checkboxValue" @change="sendChekboxValue" />
      <label for="checkbox">Full Time</label>
    </div>
    <div class="inputWrapper">
      <label class="sideInputLabel" for="">Location</label>
      <div class="inputWrapperInner">
        <i class="material-icons public">public</i>
        <input
          id="sideinput"
          v-model="sideSearchValue"
          placeholder="City, state, zip code or country"
          @change="sendSideSearchValue"
          @keyup.enter="sideSearchEnterPress"
        />
      </div>
    </div>
    <template v-for="(city, index) in cities" :key="index" >
      <input type="radio" :id="city" :value="city" v-model="pickedRadio" @change="sendRadioValue" />
      <label class="radioLabel" :for="city">{{city}}</label>
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
      this.sideSearchValue = '';
    },
  },
});
</script>

<style scoped lang="scss">
*{
  color:#334680;
}

.sideInputLabel, .public {
  color: #B9BDCF;
  font-weight: 900;
}

.public {
  position: absolute;
  top: 50%;
  left: 15px;
  color: #b9bdcf;
  transform: translate(0, -50%);
}

.inputWrapperInner {
  position: relative;
  background-color: white;
  border-radius: 4px;
  overflow: hidden;
  width: 100%;
  height: 45px;
  box-shadow: 0px 2px 4px rgba(0, 0, 0, 0.05);
}

#sideinput {
  display: block;
  width: 100%;
  height: 100%;
  margin-left: 40px;
  border: none;
  &::placeholder {
    color: #b9bdcf;
  }
  &:focus {
    outline: none;
  }
}
</style>
