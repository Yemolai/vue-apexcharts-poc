<template>
  <div class="hello">
    <h1>{{ msg }}</h1>
    <p>
      For a guide and recipes on how to configure / customize this project,<br>
      check out the
      <a href="https://cli.vuejs.org" target="_blank" rel="noopener">vue-cli documentation</a>.
    </p>
    <h3>ApexCharts</h3>
    <basic-bar-chart :x-axis="{ years }" :data="chartData" />
  </div>
</template>

<script>
import BasicBarChart from './BasicBarChart'

const years = new Array(12).fill(0).map((_, idx, a) => Number(new Date().getFullYear()) - a.length + idx)

export default {
  name: 'HelloWorld',
  components: { BasicBarChart },
  props: {
    msg: String
  },
  data: () => ({
    years,
    series: 2,
    length: 12
  }),
  computed: {
    xData () {
      const y = new Date().getFullYear()
      return new Array(this.length).fill(0).map((_, idx, a) => Number(y) - a.length + idx)
    },
    chartData () {
      const len = this.years.length
      const data = new Array(this.series).fill(0).reduce((a, c) => {
        const newData = new Array(len).fill(0)
          .map((_, idx) => Number(((Math.random() * 2) + idx).toFixed(2)))
        return { ...a, [`DataSet ${c + 1}`]: newData }
      })
      return data
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
}
a {
  color: #42b983;
}
</style>
