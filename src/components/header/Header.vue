<template>
  <div class="header">
    <div class="inputWrapper">
      <input
        class="input"
        type="text"
        placeholder="Title, companies, expertise or benefits"
        v-model="searchValue"
        @keyup.enter="sendSearchValue"
      />
      <i class="material-icons search-icon">work_outline</i>
      <Button label="Search" class="button" @buttonClicked="sendSearchValue" size="large" />
    </div>
  </div>
</template>

<script lang="ts">
import { defineComponent } from 'vue';
import Button from '../button/Button.vue';

export default defineComponent({
  data() {
    return {
      searchValue: '',
    };
  },
  components: {
    Button,
  },
  methods: {
    sendSearchValue() {
      this.$emit('mainSearchValueUpdated', this.searchValue);
      this.searchValue = '';
    },
  },
});
</script>

<style scoped lang="scss">
.header {
  background-image: url('../../assets/images/backgroundImg.png');
  background-position: center; /* Center the image */
  background-repeat: no-repeat; /* Do not repeat the image */
  background-size: cover; /* Resize the background image to cover the entire container */
  width: 100%;
  height: 140px;
  display: flex;
  align-items: center;
  justify-content: center;
}

.inputWrapper {
  position: relative;
  background-color: white;
  border-radius: 4px;
  overflow: hidden;
  width: 75%;
  height: 55px;
}

.input {
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

.search-icon {
  position: absolute;
  top: 50%;
  left: 15px;
  color: #b9bdcf;
  transform: translate(0, -50%);
}

.button {
  position: absolute;
  right: 5px;
  top: 50%;
  transform: translate(0, -50%);
  background-color: #1e86ff;
  color: white;
}
</style>
