<template>

  <div class="container">
    <img src="/images/bg-header-desktop.svg" alt="" class="bgImage"/>

    <div>
      <div class="filtersWrapper">
        <div class="filters">
          <div class="filter">
            <div>CSS</div>
            <img src="/images/icon-remove.svg" alt="" />
          </div>

          <div class="filter">
            <div>CSS</div>
            <img src="/images/icon-remove.svg" alt="" />
          </div>

          <div class="filter">
            <div>CSS</div>
            <img src="/images/icon-remove.svg" alt="" />
          </div>
        </div>

        <button class="clear">Clear</button>
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
    height: 156px;
  }

  .jobs {
    margin-top: 30px;
    padding: 40px;
    display: flex;
    flex-direction: column;
    gap: 20px;
  }

  .filtersWrapper {
    display: flex;
    justify-content: space-between;
    align-items: center;
    padding: 30px;
    margin: 0px 40px;
    margin-top: -47.5px;
    background-color: #FFFFFF;
    border-radius: 10px;
    box-shadow: rgba(91, 164, 164, 0.15) 0px 20px 25px -5px, rgba(91, 164, 164, 0.04) 0px 10px 10px -5px;
    z-index: 50;
    position: relative;
  }

  .filters {
    display: flex;
    flex-wrap: wrap;
    gap: 20px;
  }

  .filter {
    display: flex;
    align-items: center;
    background-color: hsl(180, 52%, 96%);
    color: hsl(180, 29%, 50%);
    border-radius: 4px;
    font-size: 13px;
    font-weight: bold;
    letter-spacing: -0.1px;
  }

  .filter div {
    padding: 10px;
    border-top-left-radius: 4px;
    border-bottom-left-radius: 4px;
  }

  .filter img {
    background-color: #5CA5A5;
    padding: 10px;
    height: 35px;
    width: 35px;
    border-top-right-radius: 4px;
    border-bottom-right-radius: 4px;
    cursor: pointer;
  }

  .filter img:active {
    background-color: #2B3939;
  }

  .clear {
    color: #5CA5A5;
    background: none;
    border: none;
    cursor: pointer;
    font-size: 13px;
    font-weight: bold;
    
  }

  .clear:active {
    text-decoration: underline;
  }
</style>
