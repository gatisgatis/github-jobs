<template>
  <div class="wrapper">
    <div class="row">
      <div class="col-xs-12 flex start-xs">
        <h3>{{ job.title }}</h3>
        <h4 class="jobType">{{ job.type }}</h4>
      </div>
      <div class="col-xs-12">
        <div class="flex middle-xs whenWrapper">
          <i class="material-icons public">access_time</i>
          <span class="when">{{ formatedDate }}</span>
        </div>
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
        <div class="flex middle-xs locationWrapper">
          <i class="material-icons public">public</i>
          <span class="location">{{ job.location }}</span>
        </div>
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
import moment from 'moment';
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
  padding: 20px;
  width: 100%;
}

.img-wrapper-fullJob {
  width: 100%;
}

.location,
.when {
  color: #b9bdcf;
  display: flex;
  padding-left: 10px;
}

.public {
  display: flex;
  color: #b9bdcf;
}

.locationWrapper {
  min-width: 80px;
  justify-content: space-between;
}

.jobType {
  border: 1px solid black;
  border-radius: 4px;
  margin-left: 10px;
  padding: 5px 3px;
  font-size: 0.8rem;
}
</style>
