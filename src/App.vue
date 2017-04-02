<template>
  <div id="app">
    <img src="./assets/logo.png">
    <banner @newScheduleItem="createNewScheduleItem"></banner>
    <service-schedule-item v-for='item in scheduleList' v-bind:service="item">
          </service-schedule-item>
  </div>
</template>

<script>
import Banner from './components/Banner'
import ServiceScheduleItem from './components/ServiceScheduleItem'
import axios from 'axios'

export default {
  name: 'app',
  components: {
    Banner,
    ServiceScheduleItem
  },
  created: function () {
    this.fetchScheduleList()
  },
  data () {
    return {
      scheduleList: []
    }
  },
  methods: {
    createNewScheduleItem: function () {
      this.scheduleList.push({})
    },
    fetchScheduleList: function () {
      axios.get('/static/services.get.json')
        .then((function (self) {
          return function (allServices) {
            // TODO if a new schedule item is in the array this would delete it
            self.scheduleList = allServices.data
          }
        }(this)))
        .catch(function () {
          console.error('failed to load existing scheduled services')
        })
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
