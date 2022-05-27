<template>
  <!-- Main page layout -->
  <div id="app">
    <b-container class="bv-row">
      <b-row class="header text-center">
        <b-col></b-col>
        <b-col cols="8">
          <h2>#IOT Sensor 🌡</h2>
        </b-col>
        <b-col></b-col>
      </b-row>
      <b-row class="text-center">
        <b-col></b-col>
        <b-col cols="8">
          <div class="chartbox">
            <LineChart/>
          </div>
        </b-col>
        <b-col></b-col>
      </b-row>
      <b-row class="footer text-center">
        <b-col></b-col>
        <b-col cols="8">
          <p class="footertext">
            <ul>
              <li>Built with:</li>
              <li>Vue.js</li>
              <li>InfluxDB</li>
              <li>VueBootStrap</li>
            </ul>
          </p>
          <p class="footertext">
            <ul>
              <li>Per Rawdin 1DV027 IOT</li>
            </ul>
          </p>
        </b-col>
        <b-col></b-col>
      </b-row>
    </b-container>
  </div>
</template>

<script>
/**
 *
 * App component.
 *
 * @author Per Rawdin <per.rawdin@student.lnu.se>
 * @version 1.0.0
 */
import LineChart from './components/LineChart.vue'

export default {
  name: 'App',
  components: {
    LineChart
  }
}
</script>

<style>

</style>
