<template>
  <main v-if="!loading">
    <DataTitle :text="title" :dataDate="dataDate" />
  </main>
</template>

<script>
import DataTitle from '@/components/DataTitle'
export default {
  name: 'HomeView',
  components: {
    DataTitle
  },
  data() {
    return {
      loading: true,
      title: 'Global',
      dataDate: '2022-06-06T00:52:54.553Z',
      status: {},
      countries: []
    }
  },
  methods: {
    async fetchCovidData() {
      const res = await fetch('https://api.covid19api.com/summary');
      const data = await res.json();
      return data;
    }
  },
  created() {
    const data = this.fetchCovidData();
    console.log(data);
    this.dataDate = data.Date;
    console.log(data.Date);
    this.stats = data.Global;
    this.countries = data.Countries;
    this.loading = false;
  }
}
</script>
