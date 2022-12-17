<template>
  <main v-if="!loading">
    <DataTitle :title="title" :date="dataDate" />
    <CountrySelect @get-country="GetCountryFromSelect" :countries="countries" />
    <DataBox :stats="stats" />
    <hr>
    
    <button 
    v-if="stats.Country" 
    class="min-w-auto w-32 h-10 bg-red-300 p-2 rounded-xl hover:bg-red-500 transition-colors duration-50 hover:animate-pulse ease-out text-white font-semibold"
    @click="ClearSelection()" >Clear</button>
  </main>
  <main v-else class="flex flex-col align-center justify-center">
    <div class='flex items-center justify-center min-h-screen'>
      <div style="border-top-color:transparent" class="w-8 h-8 border-4 border-blue-200 rounded-full animate-spin">
      </div>
      <p class="ml-2">Loading...</p>
    </div>
  </main>
</template>

<script>
import DataTitle from '@/components/DataTtitle';
import DataBox from '@/components/DataBox';
import CountrySelect from '@/components/CountrySelect';

export default {
  name: 'HomeView',
  components: {
    DataTitle,
    DataBox,
    CountrySelect
  },
  data() {
    return {
      loading: true,
      title: 'Global',
      dataDate: '',
      stats: {},
      countries: [],
      loadingImage: require('../assets/loading.gif'),
    }
  },
  methods: {
    async fetchCovidData() {
      const results = await fetch('https://api.covid19api.com/summary');
      const data = await results.json();
      return data;
    },
    GetCountryFromSelect(Country){
      this.stats = Country;
      this.title = Country.Country;
    },
    async ClearSelection(){
      this.loading = true;
      const data = await this.fetchCovidData();
      this.stats = data.Global;
      this.title = 'Global';
      this.loading = false;
    }
  },
  async created() {
    const data = await this.fetchCovidData();
    console.log(data);
    this.dataDate = this.dataDate = data.Date;
    this.stats = data.Global;
    this.countries = data.Countries;

    this.loading = false;
  },
}
</script>
