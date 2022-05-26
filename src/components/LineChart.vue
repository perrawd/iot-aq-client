<template>
  <div></div>
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
          this.chartOptions.xaxis.categories = response.data._embedded.dataRecordList.map(data => data.time)
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
      series: null
    }
  }
}
</script>

<style>

</style>
