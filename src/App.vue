<template>
  <div id="app">
    <main>
      <div v-if="typeof data.Global != 'undefined'">
        <div>
          Total confirmed cases: {{ data.Global.TotalConfirmed }}
        </div>
        <div>
          Total deaths: {{ data.Global.TotalDeaths }}
        </div>
                <div>
          Mortality Rate: {{ (data.Global.TotalDeaths/data.Global.TotalConfirmed * 100).toFixed(2) + '%' }}
        </div>
      </div>
        {{ data.Global }}
    </main>
  </div>
</template>

<script>
export default {
  name: 'App',
  data () {
    return {
      url: 'https://api.covid19api.com/summary',
      query: '',
      data: {}
    }
  },
  methods: {
    fetchData () {
      fetch(`${this.url}`)
      .then(res => {
        return res.json();
      }).then(this.setResults);
    },
    setResults (results) {
      this.data = results;
    }
  },
  beforeMount() {
    this.fetchData()
  }
}
</script>

<style>

</style>
