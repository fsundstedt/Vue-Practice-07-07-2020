<template>
  <div id="app">
    <main>
      <h2>Global Data</h2>
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
      <h2>Data By Country</h2>
      <div v-if="typeof data.Global != 'undefined'">
        <div>
          {{ data.Countries[0]}}
          <ul>
            <li v-for='country in data.Countries' :key='country.Country'>
              <div>
                {{ country.Country }}
              </div>
              <div>
                Total Cases: {{ country.TotalConfirmed }}
              </div>
              <div>
                Total Deaths: {{ country.TotalDeaths }}
              </div>
              <div>
                Mortality Rate: {{ ( country.TotalDeaths / country.TotalConfirmed * 100 ).toFixed(2) + '%' }}
              </div>
            </li>
          </ul>
        </div>
      </div>
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
