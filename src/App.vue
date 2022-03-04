<template>

  <div class="container">
    <img src="/images/bg-header-desktop.svg" alt="" class="bgImage"/>

    <div>
      <div v-if="filters.length" class="filtersWrapper">
        <div class="filters">
          <div :key="filter" v-for="filter in filters" class="filter">
            <div>{{ filter }}</div>
            <img src="/images/icon-remove.svg" alt="" @click="removeFilter(filter)"/>
          </div>
        </div>

        <button class="clear" @click="clearFilters">Clear</button>
      </div>
    </div>

    <div class="jobs">
      <div :key="job.id" v-for="job in filteredJobs">
        <JobListing :job="job" :addFilter="addFilter" :removeFilter="removeFilter" />
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
      allJobs: getData(),
      filteredJobs: getData(),
      filters: []
    }
  },
  watch: {
    filters: {
      handler(newFilters) {
        this.filterJobs(Object.values(newFilters))
      },
      immediate: true
    }
  },
  methods: {
    addFilter(filter) {
      if (!this.filters.includes(filter)) {
        this.filters = [filter, ...this.filters]
      }
    },
    removeFilter(filter) {
      if (this.filters.includes(filter)) {
        this.filters = this.filters.filter((f) => f !== filter)
      }
    },
    clearFilters() {
      this.filters = []
    },
    filterJobs(filters) {
      if (filters.length) {
        this.filteredJobs = this.allJobs.filter((job) => {
          for (let filter of filters) {
            if (job.role === filter) {
              continue
            }

            if (job.level === filter) {
              continue
            }

            if (job.languages && job.languages.includes(filter)) {
              continue
            }

            if (job.tools && job.tools.includes(filter)) {
              continue
            }

            return false
          }
          return job
        })
        window.scrollTo(0,0)
      } else {
        this.filteredJobs = this.allJobs
      }
    }
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
    padding: 40px;
    padding-top: 50px;
    display: flex;
    flex-direction: column;
    gap: 20px;
    margin-top: 30px;
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

  @media only screen and (max-width: 768px) {
    .filtersWrapper {
      margin: 20px;
      margin-top: -60px;
    }

    .jobs {
      padding: 20px;
      gap: 40px;
    }
  }
</style>
