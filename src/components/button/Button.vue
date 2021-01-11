<template>
  <button
    @click="$emit('buttonClicked')"
    :class="`button1 ${color} ${size} ${hideBorder && 'hideBorder'}`"
    :type="isTypeButton ? 'button' : 'submit'"
  >
    {{ label }}
  </button>
</template>

<script lang="ts">
import { defineComponent } from 'vue';

export default defineComponent({
  props: {
    label: {
      type: String,
      required: true,
      default: 'No Name',
    },
    color: {
      type: String,
      default: '',
    },
    size: {
      type: String,
      default: '',
    },
    isTypeButton: {
      type: Boolean,
      default: true,
    },
    hideBorder: {
      type: Boolean,
      default: false,
    },
  },
});
</script>

<style scoped lang="scss">
.button1 {
  padding: 8px 10px;
  border: 1px solid grey;
  color: grey;
  border-radius: 4px;
  cursor: pointer;
  background-color: transparent;
}

.large {
  width: 146px;
  padding: 15px 25px;
}

.secondary {
  color: white;
  background-color: blue;
  border-color: blue;
}

.hideBorder {
  border: none;
}

@media (max-width: 690px) {
  .large {
    width: 90px;
    padding: 15px;
  }
}
</style>
