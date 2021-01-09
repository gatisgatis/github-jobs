<template>
  <div>
    <Header @newSearchValue="searchJob" />
    <Button label="MY BYTT" @buttonClicked="handleButtonClick()" />
    <div class="RAAMIS">
      <Image imgPath="https://wallpapercave.com/wp/wp2550677.jpg" />
    </div>
    <div v-if="loading" class="row">
      LOADING.......
    </div>
    <div v-else class="row">
      <div v-for="job in jobs" :key="job.id" class="col-xs-12 margin-bottom--10">
        <Card :job="job" />
      </div>
    </div>
  </div>
</template>

<script lang="ts">
/* eslint-disable @typescript-eslint/camelcase */
import { defineComponent } from 'vue';
import axios from 'axios';
import Card from '../components/card/Card.vue';
import Button from '../components/button/Button.vue';
import Image from '../components/image/Image.vue';
import { Job } from '../types/job';
import Header from '../components/header/Header.vue';

interface Data {
  jobs: Job[];
  loading: boolean;
}

export default defineComponent({
  components: {
    Card,
    Button,
    Image,
    Header,
  },
  data(): Data {
    return {
      jobs: [],
      loading: true,
    };
  },
  methods: {
    handleButtonClick() {
      console.log('Nospiedu pogu');
    },
    searchJob(searchValue: string) {
      console.log('saņēmām piepras', searchValue);
    },
  },
  // mounted() {
  //   const accessPoint = 'https://cors-anywhere.herokuapp.com';
  //   const url = 'https://jobs.github.com/positions.json';
  //   axios.get(`${accessPoint}/${url}`).then(({ data }) => {
  //     console.log(data);
  //     data.forEach((job: Job) => {
  //       this.jobs.push({ ...job });
  //     });
  //     this.loading = false;
  //   });
  // },
});
</script>

<style scoped lang="scss">
.RAAMIS {
  width: 500px;
  background-color: red;
  border: 2px solid black;
  border-radius: 10px;
  overflow: hidden;
  box-shadow: 5px 20px 20px blue;
}
</style>
