<template>
  <div class="charts">
    <h1>Available charts</h1>

    <ul id="array-rendering">
        <li v-for="item in charts" :key="item.id">
            {{ item.name }}
            <button class="button" @click="installChart(item)">Install</button>
            <button class="button" @click="unInstallChart(item)">Uninstall</button>
        </li>
    </ul>

    <button class="button" style="display:block;margin:auto;" @click="clearLog()">Clear log</button>
    <div class="consolelog">
        <span v-for="item in console" :key="item">{{item}}</span>
    </div>

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
          charts: [],
          console:[]
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
    clearLog: function() {
        this.console = [];
    },
    logMsg: function(msg) {
        console.log(msg);
        this.console.push(msg);
    },
    logReaderToConsole: function(reader) {
        const pump = () => reader.read()
            .then(res => { 
                if (!res.done) {
                    this.logMsg(String.fromCharCode.apply(String, res.value));
                    pump(); 
                } 
            });

        pump();
    },
    installChart: function(item) {
        this.logMsg("Installing chart '" + item.id + "' with name '" + item.name.toLowerCase() + "'");
        fetch("/charts/new", { 
            method: 'POST',
            headers: { 'Content-Type': 'application/json' },
            body: JSON.stringify(item)
        })
        .then(response => response.body)
        .then(body => this.logReaderToConsole(body.getReader()))
        .catch(error => {
            console.log(error);
        });
    },
    unInstallChart: function(item) {
        this.logMsg("Uninstalling chart with name '" + item.name.toLowerCase() + "'");
        fetch("/charts/uninstall/" + item.name.toLowerCase(), { method: 'GET' })
        .then(response => response.body)
        .then(body => this.logReaderToConsole(body.getReader()))
        .catch(error => {
            console.log(error);
        });
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
  padding: 5px;
  border: #42b983 1px solid;
}
li button {
  margin: 10px;
  display: block;
}
a {
  color: #42b983;
}
.consolelog {
    color: blue;
    white-space: pre-line;
}
</style>
