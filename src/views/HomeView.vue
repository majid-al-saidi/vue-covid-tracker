<template>
  <div class="home">
    Covid Tracker
  </div>
</template>

<script>


export default {
  name: 'HomeView',
  components: {},
  methods: {
    async fetchCovidData(){
      const results = await fetch('https://api.covid19api.com/summary');
      const data = await results.json();
      return data;
    }
  },
  async created() {
    const covidData = await this.fetchCovidData();
    console.log(covidData); 
  },
}
</script>
