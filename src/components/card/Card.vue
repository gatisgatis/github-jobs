<template>
  <div class="wrapper" @click="goToJobPage()">
    <div class="row">
      <div class="col-xs-4 col-sm-2 flex middle-xs">
        <div class="img-wrapper-card">
          <Image :imgPath="job.company_logo" :alt="job.company" :isObjectFitCover="false" />
        </div>
      </div>
      <div class="col-xs-8 col-sm-6">
        <h5>{{ job.company }}</h5>
        <h2 class="title">{{ job.title }}</h2>
        <div>
          <h4 class="jobType">{{ job.type }}</h4>
        </div>
      </div>
      <div class="col-sm-4 col-xs-offset-4 col-sm-offset-0 col-xs-8 flex bottom-xs">
        <div>
          <i class="material-icons">public</i>
          <div class="location">{{ job.location }}</div>
          <i class="material-icons">access_time</i>
          <div class="when">{{ job.created_at }}</div>
        </div>
      </div>
    </div>
  </div>
</template>

<script lang="ts">
import { defineComponent } from 'vue';
import Image from '../image/Image.vue';
// import { Job } from '../../App.vue';

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
      this.$router.push(`/job/${this.job.id}`);
    },
  },
});
</script>

<style scoped lang="scss">
* {
  color: #334680;
}
.wrapper {
  width: 100%;
  background-color: white;
  border-radius: 5px;
  transition: box-shadow 0.2s;
  cursor: pointer;
  box-shadow: 0px 2px 4px rgba(0, 0, 0, 0.05);
  &:hover {
    box-shadow: 3px 3px 10px grey;
  }
}

.img-wrapper-card {
  position: relative;
  width: 100%;
  overflow: hidden;
  border-radius: 4px;
}

.title {
  cursor: pointer;
}

.location,
.when,
.material-icons {
  color: #b9bdcf;
}

.jobType {
  border: 1px solid #334680;
  border-radius: 4px;
}
</style>
