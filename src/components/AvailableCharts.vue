<template>
  <div class="charts">
    <h1>Available charts</h1>

    <ul id="array-rendering">
        <li v-for="item in charts" :key="item.id">
            {{ item.name }}
            <button class="button" style="display:block;margin:auto;" @click="installChart(item)">Install</button>
        </li>
    </ul>

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
  mounted() {
      this.$nextTick(() => {
        this.getCharts();
      });
  },
  methods: {
    getCharts: function() {
        console.log("Invoking get charts endpoint");
        axios.get("/charts")
            .then(response => {this.charts = response.data})
    },
    installChart: function(item) {
        console.log("Installing " + item.id);  
        axios.post("/charts/new", item)
            .then(response => console.log(response));
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
  display: inline-block;
  margin: 0 10px;
  border: #42b983 1px solid;
}
a {
  color: #42b983;
}
</style>
