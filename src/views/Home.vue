<template>
  <div>
    <Header @mainSearchValueUpdated="updateMainSearchInputValue" class="margin-bottom--30" />
    <div class="row">
      <div class="col-xs-4">
        <SideSearch
          @sideSearchValueUpdated="updateSideSearchInputValue"
          @checkboxValueUpdated="updateChekboxValue"
          @radioValueUpdated="updateRadioValue"
          @sideSearchEnterPressed="filterJobs"
        />
      </div>
      <div class="col-xs-8">
        <div v-if="loading" class="row">
          LOADING.......
        </div>
        <div v-else class="row">
          <div v-for="job in jobs" :key="job.id" class="col-xs-12 margin-bottom--10">
            <Card :job="job" />
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script lang="ts">
/* eslint-disable @typescript-eslint/camelcase */
import { defineComponent } from 'vue';
import axios from 'axios';
import Card from '../components/card/Card.vue';
import { Job } from '../types/job';
import Header from '../components/header/Header.vue';
import SideSearch from '../components/sideSearch/SideSearch.vue';

interface Data {
  sideSearchInputValue: string;
  jobs: Job[];
  loading: boolean;
  checkboxValue: boolean;
  radioValue: string;
  mainSearchInputValue: string;
  totalSearchValue: string;
}

export default defineComponent({
  components: {
    Card,
    Header,
    SideSearch,
  },
  data(): Data {
    return {
      sideSearchInputValue: '',
      jobs: [],
      loading: true,
      checkboxValue: false,
      radioValue: '',
      mainSearchInputValue: '',
      totalSearchValue: '',
    };
  },
  methods: {
    updateMainSearchInputValue(value: string) {
      this.mainSearchInputValue = value;
      this.filterJobs();
    },
    updateSideSearchInputValue(value: string) {
      this.sideSearchInputValue = value;
    },
    updateChekboxValue(value: boolean) {
      this.checkboxValue = value;
    },
    updateRadioValue(value: string) {
      this.radioValue = value;
    },
    filterJobs() {
      this.totalSearchValue = `https://jobs.github.com/positions.json?${
        this.mainSearchInputValue ? `description=${this.mainSearchInputValue}` : ''
      }${
        this.mainSearchInputValue
          ? `&full_time=${this.checkboxValue}`
          : `full_time=${this.checkboxValue}`
      }${this.sideSearchInputValue ? `&location=${this.sideSearchInputValue}` : ''}`;
      console.log(
        this.sideSearchInputValue,
        this.checkboxValue,
        this.radioValue,
        this.mainSearchInputValue,
        this.totalSearchValue,
      );
      // uzģenerēt jaunu API linku
      // Uztaisit axios call
      // nomainit loading state
      // update job state
      // noņemt loading state
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

<style scoped lang="scss"></style>
