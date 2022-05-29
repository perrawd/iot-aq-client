<template>
  <div>
    <h4>Current</h4>
    <b-row>
      <b-col></b-col>
      <b-col>
        <b-card :title="currentTemp" sub-title="🌡 Temperature"></b-card>
      </b-col>
      <b-col>
        <b-card :title="currentHumidity" sub-title="💧 Humidity"></b-card>
      </b-col>
      <b-col></b-col>
    </b-row>
    <p>Current measurement gathered on: {{currentTime}}</p>
    <hr>
    <h4>Historical data</h4>
    <!-- Display chart if data has been loaded sucessfully -->
    <div v-if="series" class="linechart">
      <apexcharts type="line" :options="chartOptions" :series="series" />
    </div>
    <!-- Else display loading spinner. -->
    <div v-else class="d-flex justify-content-center mb-3 loading">
      <b-spinner />
    </div>
  </div>
</template>

<script>
/**
 *
 * LineChart component.
 *
 * @author Per Rawdin <per.rawdin@student.lnu.se>
 * @version 1.0.0
 */
import VueApexCharts from 'vue-apexcharts'
import axios from 'axios'

export default {
  name: 'LineChart',
  components: {
    apexcharts: VueApexCharts
  },
  mounted () {
    // Fetch data from API.
    axios.get(process.env.VUE_APP_URL, {
      auth: {
        username: process.env.VUE_APP_USER,
        password: process.env.VUE_APP_PASS
      }
    })
    // Map response data to object variable.
      .then(
        (response) => {
          this.results = response.data._embedded.dataRecordList
          this.chartOptions.xaxis.categories = response.data._embedded.dataRecordList.map(data => new Date(data.time).toLocaleString('sv-SE'))
          this.currentTemp = this.results[this.results.length - 1].temperature.toString()
          this.currentHumidity = this.results[this.results.length - 1].humidity.toString()
          this.currentTime = new Date(this.results[this.results.length - 1].time.toString()).toLocaleString('sv-SE')

          this.series = [
            {
              name: 'Temperature',
              data: response.data._embedded.dataRecordList.map(data => data.temperature)
            },
            {
              name: 'Humidity',
              data: response.data._embedded.dataRecordList.map(data => data.humidity)
            }
          ]
        }
      )
      .catch((error) => console.error(error.message))
  },
  data () {
    return {
      results: null,
      // Chart configuration.
      chartOptions: {
        stroke: {
          curve: 'smooth'
        },
        chart: {
          id: 'basic-bar'
        },
        xaxis: {
          categories: null
        }
      },
      series: null,
      currentTemp: null,
      currentHumidity: null,
      currentTime: null
    }
  }
}
</script>
