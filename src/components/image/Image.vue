<template>
  <div class="img-wrapper" :style="{ paddingTop: paddingTopFromProps }">
    <img class="img" :src="imgPath" :alt="alt" :class="!isObjectFitCover && 'contain'" />
  </div>
</template>

<script lang="ts">
import { defineComponent } from 'vue';

export default defineComponent({
  props: {
    imgPath: {
      type: String,
      required: true,
    },
    AspectRatio: {
      type: Number,
      default: 1,
    },
    alt: {
      type: String,
      default: 'No Info',
    },
    isObjectFitCover: {
      type: Boolean,
      default: true,
    },
  },
  computed: {
    paddingTopFromProps(): string {
      return `${(this.AspectRatio * 100).toFixed(2)}%`;
    },
  },
});
</script>

<style scoped lang="scss">
.img-wrapper {
  position: relative;
  line-height: 0;
  width: 100%;
}

.img {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  object-fit: cover;
}

.contain {
  object-fit: contain;
}
</style>
