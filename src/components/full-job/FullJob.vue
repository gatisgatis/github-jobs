<template>
  <div class="wrapper">
    <div class="row">
      <div class="col-xs">
        <h3>{{ job.title }}</h3>
      </div>
      <div class="col-xs flex middle-xs start-xs">
        <h4>{{ job.type }}</h4>
      </div>
    </div>
    <div class="when">{{ job.created_at }}</div>
    <div class="row">
      <div class="col-xs-1">
        <div class="img-wrapper-fullJob">
          <Image :imgPath="job.company_logo" :alt="job.company" :isObjectFitCover="false"/>
        </div>
      </div>
      <div class="col-xs-1">
        <h3>{{ job.company }}</h3>
        <div class="location">{{ job.location }}</div>
      </div>
    </div>
    <p v-html="job.description" />
  </div>
</template>

<script lang="ts">
import { defineComponent } from 'vue';
import Image from '../image/Image.vue';

export default defineComponent({
  components: {
    Image,
  },
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
  width: 100%;
}

.img-wrapper-fullJob {
  width: 100%;
}

.location, .when {
  color: #B9BDCF;
}
</style>
