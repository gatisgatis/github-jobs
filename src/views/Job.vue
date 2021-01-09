<template>
  <div>
    <h1>This is an job page</h1>
    <h2>{{ id }}</h2>
    <div v-if="loading">
      LOADING....
    </div>
    <div>
      <input type="text" name="" id="" />
      <FullJob :job="job" />
    </div>
  </div>
</template>

<script lang="ts">
/* eslint-disable @typescript-eslint/camelcase */
import { defineComponent } from 'vue';
import axios from 'axios';
import FullJob from '../components/full-job/FullJob.vue';
import { Job } from '../types/job';

interface Data {
  job: Job;
  loading: boolean;
}

export default defineComponent({
  data(): Data {
    return {
      loading: true,
      job: {},
    };
  },
  computed: {
    id(): string | string[] {
      return this.$route.params.id;
    },
  },
  components: {
    FullJob,
  },
  mounted() {
    axios.get(`https://jobs.github.com/positions/${this.id}.json`).then(({ data }) => {
      this.job = { ...data };
      this.loading = false;
    });
  },
});
</script>
