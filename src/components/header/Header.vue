<template>
  <div class="header">
    <div class="inputWrapper">
      <input
        class="input"
        type="text"
        placeholder="Title, companies, expertise or benefits"
        v-model="searchValue"
      />
      <Button label="Search" class="button" @buttonClicked="sendSearchValue" />
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
      this.$emit('newSearchValue', this.searchValue);
      this.searchValue = '';
    },
  },
});
</script>

<style scoped>
.header {
  background-image: url('../../assets/images/backgroundImg.png');
  width: 100%;
  height: 100px;
  display: flex;
  align-items: center;
  justify-content: center;
}

.inputWrapper {
  position: relative;
}

.input {
  display: block;
  max-width: 800px;
  width: 100%;
  min-height: 50px;
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

// :modelValue="inputValue" // @input="$emit('update:modelValue', $event.target.value)"
