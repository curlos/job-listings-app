<template>

  <div class="container">
    <img src="/assets/images/bg-header-desktop.svg" alt="" class="bgImage"/>

    <div class="filters">
      <div class="filter">
        <div>CSS</div>
        <img src="/images/icon-remove.svg" alt="" />
      </div>
    </div>

    <div class="jobs">
      <div :key="job.id" v-for="job in jobs">
        <JobListing :job="job"/>
      </div>
    </div>
  </div>
</template>

<script>
import JobListing from './components/JobListing'
import { getData } from './utils/getData.js'

export default {
  name: 'App',
  components: {
    JobListing
  },
  data() {
    return {
      jobs: getData()
    }
  },
  mounted() {
    console.log(this.jobs)
  }
}
</script>

<style>
  @import url('https://fonts.googleapis.com/css2?family=Spartan:wght@500;700&display=swap');

  * {
    box-sizing: border-box;
    margin: 0;
  }

  .container {
    background-color: hsl(180, 52%, 96%);
    min-height: 100vh;
    margin: 0;
    width: 100vw;
    max-width: 100%;
    font-family: Spartan, sans-serif;
  }

  .bgImage {
    background-color: hsl(180, 29%, 50%);
    object-fit: cover;
    width: 100%;
  }

  .jobs {
    margin-top: 30px;
    padding: 40px;
    display: flex;
    flex-direction: column;
    gap: 20px;
  }

  .filters {
    padding: 40px;
    margin: 0px 40px;
    background-color: #FFFFFF;
    border-radius: 10px;
  }

  .filter {
    background-color: hsl(180, 52%, 96%);
    color: hsl(180, 29%, 50%);
  }
</style>
