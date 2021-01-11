<template>
  <div class="img-wrapper" :style="{ paddingTop: paddingTopFromProps }">
    <Loader class="load" v-if="loading" />
    <div class="NoImage" v-if="imgPath === null">Not found</div>
    <img
      @load="loading = false"
      class="img"
      :src="imgPath"
      :alt="alt"
      :class="!isObjectFitCover && 'contain'"
      v-else
    />
  </div>
</template>

<script lang="ts">
import { defineComponent } from 'vue';
import Loader from '../loader/loader.vue';

export default defineComponent({
  data() {
    return {
      loading: true,
    };
  },
  components: {
    Loader,
  },
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
  mounted() {
    if (this.imgPath === null) this.loading = false;
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

.load {
  position: absolute;
  top: 0;
  left: 0;
}

.contain {
  object-fit: contain;
}

.NoImage {
  position: absolute;
  display: flex;
  align-items: center;
  justify-content: center;
  top: 50%;
  left: 50%;
  width: 100%;
  height: 100%;
  transform: translate(-50%, -50%);
  background-color: #f2f2f2;
  color: #bdbdbd;
}
</style>
