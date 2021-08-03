<template>
  <div class="charts">
    <h1>Available charts</h1>

    <ul id="array-rendering">
        <li v-for="item in charts" :key="item.id">
            {{ item.name }}
        </li>
    </ul>

    <button class="button" style="display:block;margin:auto;" @click="getCharts">Get available charts</button>

  </div>

</template>

<script>
import axios from 'axios'

export default {
  name: 'AvailableCharts',
  props: {
    msg: String
  },
  data() {
      return {
          charts: []
      }
  },
  methods: {
    getCharts: function() {
        console.log("Invoking get charts endpoint");
        axios.get("/charts")
            .then(response => {this.charts = response.data})
    }
}
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: block;
  margin: 0 10px;
  border: #42b983 1px solid;
}
a {
  color: #42b983;
}
</style>
