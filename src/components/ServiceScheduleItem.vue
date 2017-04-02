<template>
  <div class="service-schedule-item">
    <div v-if="!editing">
      <h2>{{service.commandText}}</h2>
      <div> {{service.dynoSize}} - {{service.frequency}} - {{service.lastRun}} - {{service.nextDue | prettyUtcDate}}</div>
      <button v-on:click="toggleEditingStatus">Edit</button>
      <button>Remove</button>
    </div>

    <div v-if="editing">
      <div>$<input v-bind:value="service.commandText" /></div>
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
      <button v-on:click="toggleEditingStatus">Save</button>
      <button v-if="service.id">Cancel</button>
    </div>
  </div>
</template>

<script>
export default {
  name: 'service-schedule-item',
  props: ['service'],
  data () {
    return {
      editing: false,
      tomorrowDate: (new Date()).setUTCDate((new Date()).getUTCDate() + 1)
    }
  },
  methods: {
    toggleEditingStatus: function () {
      this.editing = !this.editing
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
