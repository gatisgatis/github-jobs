<template>
  <div class="wrapper" @click="goToJobPage()">
    <div class="row">
      <div class="col-xs-4 col-sm-2 flex top-xs">
        <div class="img-wrapper-card">
          <Image :imgPath="job.company_logo" :alt="job.company" :isObjectFitCover="false" />
        </div>
      </div>
      <div class="col-xs-8 col-sm-6 flex dir-col between-xs">
        <div class="company">{{ job.company }}</div>
        <div class="title">{{ job.title }}</div>
        <div>
          <div class="jobType">{{ job.type }}</div>
        </div>
      </div>
      <div class="col-sm-4 col-xs-offset-4 col-sm-offset-0 col-xs-8 flex bottom-xs between-xs">
        <div class='flex middle-xs'>
          <i class="material-icons icon">public</i>
          <span class="location">{{ job.location.substring(0, 12) }}</span>
        </div>
        <div class='flex middle-xs'>
          <i class="material-icons icon">access_time</i>
          <span class="when">{{ formatedDate }}</span>
        </div>
      </div>
    </div>
  </div>
</template>

<script lang="ts">
import { defineComponent } from 'vue';
import moment from 'moment';
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
  computed: {
    formatedDate(): string {
      return moment(this.job.created_at).fromNow();
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
  padding: 12px;
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

.location,
.when,
.material-icons {
  color: #b9bdcf;
}
.title {
  font-size: 18px;
  color: #334680;
}
.company {
  font-size: 12px;
  color: #334680;
}

.icon {
  margin-right: 10px;
}

.jobType {
  display: inline-block;
  border: 1px solid #334680;
  padding: 5px 10px;
  border-radius: 4px;
  margin-bottom: 10px;
}
</style>
