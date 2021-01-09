<template>
  <Button label="add kautko" />
  <div class="wrapper">
    <div class="img-wrapper">
      <img class="img" :src="job.company_logo" :alt="job.company" />
    </div>
    <div>
      <h5>{{ job.company }}</h5>
      <h2 class='title' @click="goToJobPage()">{{ job.title }}</h2>
      <div>
        <h4>{{ job.type }}</h4>
      </div>
    </div>
    <div>
      <div>
        <span>{{ job.location }}</span>
        <span>{{ job.created_at }}</span>
      </div>
    </div>
  </div>
</template>

<script lang="ts">
import { defineComponent } from 'vue';
import Button from '../button/Button.vue';
// import { Job } from '../../App.vue';

export default defineComponent({
  components: {
    Button,
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
    //   this.$router.push('/job');
    },
  },
});
</script>

<style scoped lang="scss">
.wrapper {
  border: 2px solid red;
  width: 500px;
  height: 200px;
  display: flex;
}

.img-wrapper {
  position: relative;
  width: 150px;
  height: 150px;
}

.img {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  object-fit: cover;
}

.title {
  cursor: pointer;
}
</style>
