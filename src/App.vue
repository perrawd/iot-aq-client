<template>
  <!-- Main page layout -->
  <div id="app">
    <b-container class="bv-row">
      <b-row class="header text-center">
        <b-col></b-col>
        <b-col cols="8">
          <h2>Temperature and Humidity Sensor</h2>
        </b-col>
        <b-col></b-col>
      </b-row>
      <b-row class="text-center">
        <b-col></b-col>
        <b-col cols="8">
          <div class="descriptiontext">
            <p>
              Temperature and humidity data is collected and sent from a DMT11 sensor connected to a lopy4 microcontroller.
              The sensor data is sent to pybytes which in turn sends the data through webhooks to an API built in SpringBoot.
              The data is stored in influxDB and later fetched from the API to this client. <a href="">Gitlab project</a>
            </p>
          </div>
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
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}

.chartbox {
  margin: auto;
}

.btn {
  margin: 5px;
}

ul {
  list-style-type: none;
  padding: 0;
  margin: 0;
}

.footertext {
  font-size: 11px;
}
</style>
