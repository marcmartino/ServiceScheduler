<template>
  <div class="service-schedule-item">
    <div>
      <h2>{{service.commandText}}</h2>
      <div> {{service.dynoSize}} - {{service.frequency}} - {{service.lastRun}} - {{service.nextDue | prettyUtcDate}}</div>
      <button>Edit</button>
      <button>Remove</button>
    </div>


  </div>
</template>

<script>
export default {
  name: 'service-schedule-item',
  props: ['service'],
  filters: {
    prettyUtcDate: function (val) {
      return (new Date(val)).toUTCString()
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
