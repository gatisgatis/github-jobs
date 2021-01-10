<template>
  <div>
    <Header @mainSearchValueUpdated="updateMainSearchInputValue" class="margin-bottom--30" />
    <Button
      v-for="num in [1, 2, 3, 4, 5, 6, 7, 8, 9]"
      :key="num"
      :label="num"
      @buttonClicked="() => changePageNumber(num)"
    />
    <h1>{{ pageNumber }}</h1>
    <h2>{{ jobsCount }}</h2>
    <div class="row">
      <div class="col-xs-12 col-sm-4">
        <SideSearch
          @sideSearchValueUpdated="updateSideSearchInputValue"
          @checkboxValueUpdated="updateChekboxValue"
          @radioValueUpdated="updateRadioValue"
          @sideSearchEnterPressed="filterJobs"
        />
      </div>
      <div class="col-xs-12 col-sm-8">
        <div v-if="loading" class="row">
          LOADING.......
        </div>
        <div v-else class="row">
          <h1 v-if="!jobsCount">Found nothing</h1>
          <div v-else v-for="job in jobsToShow" :key="job.id" class="col-xs-12 margin-bottom--10">
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
import Button from '../components/button/Button.vue';

interface Data {
  sideSearchInputValue: string;
  jobs: Job[];
  loading: boolean;
  checkboxValue: boolean;
  radioValue: string;
  mainSearchInputValue: string;
  totalSearchValue: string;
  pageNumber: number;
  urlPageNumber: number;
}

export default defineComponent({
  components: {
    Card,
    Header,
    SideSearch,
    Button,
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
      pageNumber: 1,
      urlPageNumber: 1,
    };
  },
  methods: {
    changePageNumber(newPageNumber: number) {
      this.pageNumber = newPageNumber;
    },
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
      }${
        this.sideSearchInputValue
          ? `&location=${this.sideSearchInputValue}`
          : `${this.radioValue ? `&location=${this.radioValue}` : ''}`
      }`;
      this.mainSearchInputValue = '';
      this.sideSearchInputValue = '';
      this.loading = true;
      const accessPoint = 'https://cors-anywhere.herokuapp.com';
      axios.get(`${accessPoint}/${this.totalSearchValue}`).then(({ data }) => {
        this.jobs = [];
        data.forEach((job: Job) => {
          this.jobs.push({ ...job });
        });
        this.loading = false;
      });
    },
  },
  mounted() {
    const accessPoint = 'https://cors-anywhere.herokuapp.com';
    const url = `https://jobs.github.com/positions.json?page=${this.urlPageNumber}`;
    axios.get(`${accessPoint}/${url}`).then(({ data }) => {
      console.log(data);
      data.forEach((job: Job) => {
        this.jobs.push({ ...job });
      });
      this.loading = false;
    });
  },
  computed: {
    jobsToShow(): Job[] {
      return this.jobs.slice((this.pageNumber - 1) * 5, this.pageNumber * 5);
    },
    jobsCount(): number {
      return this.jobs.length;
    },
    // pageButtons(): number[] {
    // },
  },
});
</script>

<style scoped lang="scss"></style>
