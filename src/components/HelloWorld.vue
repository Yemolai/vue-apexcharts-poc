<template>
  <div class="hello">
    <h3>ApexCharts</h3>
    <input type="number" v-model="strSeries">
    <input type="number" v-model="strLength">
    <basic-bar-chart width="50%" :x-axis="{ years }" :data="chartData" />
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
    series: 1,
    length: 5
  }),
  computed: {
    strLength: {
      get () {
        return `${this.length}`
      },
      set (val) {
        this.length = Number(val)
      }
    },
    strSeries: {
      get () {
        return `${this.series}`
      },
      set (val) {
        this.series = Number(val)
      }
    },
    xData () {
      const y = new Date().getFullYear()
      return new Array(this.length).fill(0).map((_, idx, a) => Number(y) - a.length + idx)
    },
    chartData () {
      const data = new Array(this.series).fill(1).reduce((a, _, k) => {
        const newData = new Array(this.length)
          .fill(0)
          .map((_, idx) => Number(((Math.random() * 2) + idx).toFixed(1)))
        return { ...a, [`DataSet ${k + 1}`]: newData }
      }, {})
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
