<template>
  <div class="wrapper">
    <div class="row">
      <div class="col-xs-12 flex start-xs">
        <h3>{{ job.title }}</h3>
        <h4>{{ job.type }}</h4>
      </div>
      <div class="col-xs-12">
        <div class="when">{{ job.created_at }}</div>
      </div>
    </div>
    <div class="row middle-xs">
      <div class="col-xs-2 col-sm-1">
        <div class="img-wrapper-fullJob">
          <Image :imgPath="job.company_logo" :alt="job.company" :isObjectFitCover="false" />
        </div>
      </div>
      <div class="col-xs-10 col-sm-11 top-xs flex dir-col">
        <h3>{{ job.company }}</h3>
        <div class="location">{{ job.location }}</div>
      </div>
    </div>
    <div class="row">
      <div class="col-xs-12">
        <p v-html="job.description" />
      </div>
    </div>
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
  padding: 20px;
  width: 100%;
}

.img-wrapper-fullJob {
  width: 100%;
}

.location,
.when {
  color: #b9bdcf;
}
</style>
