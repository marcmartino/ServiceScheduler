<template>
  <div class="banner">
    <h1>{{ message }}</h1>
    <h3>
      <button v-on:click="this.addNewScheduleItem">
        Create new scheduled item</button>
    </h3>
  </div>
</template>

<script>
export default {
  name: 'banner',
  methods: {
    addNewScheduleItem: function () {
      console.log('new item adding')
      this.$emit('newScheduleItem')
    }
  },
  data () {
    return {
      message: 'Welcome to Marc\'s service scheduler test'
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
