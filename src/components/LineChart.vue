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
import axios from 'axios'
export default {
  name: 'LineChart',
  mounted () {
    // Fetch data from API.
    axios.get(process.env.VUE_APP_URL, {
      auth: {
        username: process.env.VUE_APP_USER,
        password: process.env.VUE_APP_PASS
      }
    })
  }
}
</script>

<style>

</style>
