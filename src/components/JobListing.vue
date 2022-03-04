<template>
  <div :class="{'wrapperContainer': true, 'featuredListing': job.featured}">
    <div class="wrapper">
      <div class="left">
        <img :src="job.logo.slice(1,)" alt="job.company" />
        <div class="leftDetails">
          <div class="companyAndDate">
            <div class="company">{{ job.company }}</div>
            <button v-if="job.new" class="new">NEW!</button>
            <button v-if="job.featured" class="featured">FEATURED</button>
          </div>
          <div class="position">{{ job.position }}</div>
          <div class="info">
            <div>{{ job.postedAt }}</div>
            <div class="circle" />
            <div>{{ job.contract }}</div>
            <div class="circle"/>
            <div>{{ job.location }}</div>
          </div>
        </div>
        
      </div>

      <div class="right">
        <div :key="filter" v-for="filter in filters" class="filter" @click="addFilter(filter)">
          {{ filter }}
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'JobListing',
  props: {
    job: Object,
    addFilter: Function,
    removeFilter: Function
  },
  data() {
    return {
      filters: [],
    }
  },
  mounted() {
    let endFilters = []

    if (this.job.role) {
      endFilters.push(this.job.role)
    }

    if (this.job.level) {
      endFilters.push(this.job.level)
    }

    if (this.job.languages) {
      this.job.languages.forEach((language) => endFilters.push(language))
    }

    if (this.job.tools) {
      this.job.tools.forEach((tool) => endFilters.push(tool))
    }
    
    this.filters = endFilters
  }
}
</script>

<style scoped>
  .wrapperContainer {
    border-left: 5px solid #FFFFFF;
    border-top-left-radius: 10px;
    border-bottom-left-radius: 10px;
    box-shadow: rgba(91, 164, 164, 0.15) 0px 20px 25px -5px, rgba(91, 164, 164, 0.04) 0px 10px 10px -5px;
  }

  .featuredListing {
    border-color: #5CA5A5;
  }

  .wrapper {
    border-radius: 10px;
    border-top-left-radius: 0px;
    border-bottom-left-radius: 0px;
    background-color: #FFFFFF;
    padding: 20px;
    display: flex;
    justify-content: space-between;
    align-items: center;
    gap: 50px;
  }

  .left {
    display: flex;
    align-items: center;
    gap: 10px;
  }

  .leftDetails {
    display: flex;
    flex-direction: column;
    gap: 10px;
  }

  .right {
    display: flex;
    flex-wrap: wrap;
    align-items: center;
    gap: 10px;
  }

  .filter {
    background-color: hsl(180, 52%, 96%);
    color: #5CA5A5;
    padding: 10px;
    border-radius: 10px;
    font-size: 13px;
    letter-spacing: -0.1px;
    font-weight: bold;
    cursor: pointer;
  }

  .filter:active {
    background-color: #5CA5A5;
    color: #FFFFFF;
  }

  .position {
    font-weight: bold;
    font-size: 18px;
    color: #2B3939;
    cursor: pointer;
  }

  .position:active {
    color: #5CA5A5;
  }

  .companyAndDate {
    display: flex;
    align-items: center;
    gap: 10px;
  }

  .companyAndDate button {
    border-radius: 12px;
    padding: 10px;
    font-size: 11px;
    letter-spacing: -0.08px;
    font-weight: bold;
    color: #FFFFFF;
    border: none;
  }

  .company {
    font-size: 14px;
    font-weight: bold;
    color: #5CA5A5;
  }

  .new {
    background-color: #5CA5A5;
  }

  .featured {
    background-color: #2B3939;
  }

  .info {
    display: flex;
    align-items: center;
  }

  .info div {
    color: #7C8F8F;
    font-size: 15px;
    letter-spacing: -0.12px;
    margin-right: 10px;
  }

  .circle {
    height: 4px;
    width: 4px;
    background-color: #B7C4C4;
    border-radius: 50%;
  }

  @media only screen and (max-width: 768px) {
    .wrapper {
      display: block;

    }

    .left {
      display: block;
      margin-top: -44px;
    }

    .left img {
      height: 48px;
      width: 48px;
      position: relative;
    }

    .position {
      font-size: 15px;
    }

    .info span {
      font-size: 13px;
    }

    .right {
      margin-top: 15px;
      border-top: 1px solid #B7C4C4;
      padding-top: 15px;
    }

    .filter {

    }
  }
</style>