<template>
  <div class="service-schedule-item">
    <div v-if="!editing">
      <h2>{{service.commandText}}</h2>
      <div> {{service.dynoSize}} - {{service.frequency}} - {{service.lastRun}} - {{service.nextDue | prettyUtcDate}}</div>
      <button v-on:click="toggleEditingStatus">Edit</button>
      <button>Remove</button>
    </div>

    <div v-if="editing">
      <div>$<input v-model:value="service.commandText" /></div>
      <div>
        Last Ran: <span>{{service.lastRun}}</span> -
        Frequency: <select v-model="service.frequency">
          <option>Default</option>
          <option value='daily'>Daily</option>
          <option value='hourly'>Hourly</option>
        </select> -
        Estimated Start:
        {{estimatedStart | prettyUTCDate}}

        Dyno Size:
        <select v-model="service.dynoSize">
          <option>default</option>
          <option>1X</option>
          <option>2X</option>
        </select>
      </div>
      <button v-on:click="saveItem">{{this.saving ? 'Saving...' : 'Save'}}</button>
    </div>
  </div>
</template>

<script>
import axios from 'axios'

export default {
  name: 'service-schedule-item',
  props: ['service'],
  data () {
    return {
      editing: false,
      saving: false,
      tomorrowDate: (new Date()).setUTCDate((new Date()).getUTCDate() + 1)
    }
  },
  methods: {
    toggleEditingStatus: function () {
      this.editing = !this.editing
    },
    saveItem: function () {
      this.saving = true
      // TODO id of 0 will get punted and this is rather inelegant anyway
      let targetUrl = this.service.id ? '/static/services.put.json' : '/static/services.post.json'
      axios.get(targetUrl, this.service)
        .then(function (self) {
          return function (savedServiceResp) {
            if (!self.service.id) {
              self.service.id = savedServiceResp.data.id
            }
            self.editing = false
            self.saving = false
          }
        }(this))
        .catch(function (self) {
          return function () {
            console.error('failed to save item')
            alert('Item could not be saved')
            this.saving = false
          }
        }(this))
    }
  },
  created: function () {
    if (!this.service.id) {
      this.editing = true
    }
  },
  filters: {
    prettyUtcDate: function (val) {
      return (new Date(val)).toUTCString()
    }
  },
  computed: {
    estimatedStart: function () {
      if (this.service.frequency) {
        return 1491011288018
      } else {
        return new Date()
      }
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h1, h2 {
  font-weight: normal;
}

ul {
  list-style-type: none;
  padding: 0;
}

li {
  display: inline-block;
  margin: 0 10px;
}

a {
  color: #42b983;
}
</style>
