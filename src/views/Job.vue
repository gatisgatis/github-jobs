<template>
  <div>
    <div class="container">
      <template v-if="loading" class='flex center-xs'>
        <Loader />
      </template>
      <template v-else>
        <div class="row">
          <div class="col-xs-12 col-sm-3">
            <HowToApply :howToApply="job.how_to_apply" />
          </div>
          <div class="col-xs-12 col-sm-9">
            <FullJob :job="job" />
          </div>
        </div>
      </template>
    </div>
  </div>
</template>

<script lang="ts">
import { defineComponent } from 'vue';
import axios from 'axios';
import FullJob from '../components/full-job/FullJob.vue';
import HowToApply from '../components/howToApply/HowToApply.vue';
import Loader from '../components/loader/loader.vue';
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
    HowToApply,
    Loader,
  },
  mounted() {
    const accessPoint = 'https://cors-anywhere.herokuapp.com';
    axios
      .get(`${accessPoint}/https://jobs.github.com/positions/${this.id}.json`)
      .then(({ data }) => {
        this.job = { ...data };
        this.loading = false;
      });
  },
});
</script>
