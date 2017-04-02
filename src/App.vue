<template>
  <div id="app">
    <img src="./assets/logo.png">
    <banner></banner>
    <service-schedule-item v-for='item in scheduleList' v-bind:service="item">
          </service-schedule-item>
  </div>
</template>

<script>
import Banner from './components/Banner'
import ServiceScheduleItem from './components/ServiceScheduleItem'

export default {
  name: 'app',
  components: {
    Banner,
    ServiceScheduleItem
  },
  data () {
    return {
      scheduleList: [
        {
          'id': 33491,
          'commandText': 'rake do_something',
          'dynoSize': '1X',
          'frequency': 'daily',
          'lastRun': 'never',
          'nextDue': 1491010288018
        },
        {
          'id': 33492,
          'commandText': 'rake test something',
          'dynoSize': '1X',
          'frequency': 'daily',
          'lastRun': 'yesterday',
          'nextDue': 1491011288018
        }
      ]
    }
  }
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
