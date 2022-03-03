<template>
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
          <span>{{ job.postedAt }}</span>
          <span class="circle"></span>
          <span>{{ job.contract }}</span>
          <span class="circle"/>
          <span>{{ job.location }}</span>
        </div>
      </div>
      
    </div>

    <div class="right">
      <div :key="tool" v-for="tool in job.tools" class="tool">
        {{ tool }}
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'JobListing',
  props: {
    job: Object
  }
}
</script>

<style scoped>
  .wrapper {
    border-radius: 10px;
    background-color: #FFFFFF;
    padding: 20px;
    display: flex;
    justify-content: space-between;
    align-items: center;
    box-shadow: 0px 6px 16px hsl(180, 29%, 50%);
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

  .tool {
    background-color: hsl(180, 52%, 96%);
    color: #5CA5A5;
    padding: 10px;
    border-radius: 10px;
    font-size: 13px;
    letter-spacing: -0.1px;
    font-weight: bold;
  }

  .position {
    font-weight: bold;
    font-size: 18px;
    color: #2B3939;
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

  .info span {
    color: #7C8F8F;
    font-size: 15px;
    letter-spacing: -0.12px;
    margin-right: 10px;
  }

  .circle {
    height: 4px;
    width: 4px;
    color: red;
    border-radius: 50%;
  }
</style>