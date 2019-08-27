<template>
  <div class="hello">
    <h3>ApexCharts</h3>
    <input type="number" v-model="strProgress">
    <input type="number" v-model="strSeries">
    <input type="number" v-model="strLength">
    <div class="row">
      <div style="width: 33.3%">
        <progress-indicator
          name="Indicator"
          :value="progress || 0"
          width="60%"
          start-at="top"/>
      </div>
      <div style="width: 33.3%">
        <area-chart :data="chartData" />
      </div>
      <div style="width: 33.3%">
        <stacked-col-chart :data="chartData" percentage />
      </div>
    </div>
    <div class="row">
      <div style="width: 50%"></div>
      <div style="width: 50%"></div>
    </div>
    <div class="row">
      <div style="width: 50%">
        <basic-bar-chart :x-axis="{ years }" :data="chartData" />
      </div>
      <div style="width: 50%">
        <basic-line-chart :x-axis="{ years }" :data="chartData" />
      </div>
    </div>
  </div>
</template>

<script>
import BasicBarChart from './BasicBarChart'
import BasicLineChart from './BasicLineChart'
import ProgressIndicator from './ProgressIndicator'
import AreaChart from './AreaChart'
import StackedColChart from './StackedColChart'

const years = new Array(12).fill(0).map((_, idx, a) => Number(new Date().getFullYear()) - a.length + idx)

export default {
  name: 'HelloWorld',
  components: {
    BasicBarChart,
    BasicLineChart,
    AreaChart,
    ProgressIndicator,
    StackedColChart
  },
  props: {
    msg: String
  },
  data: () => ({
    years,
    progress: 95.64,
    series: 1,
    length: 5
  }),
  computed: {
    strProgress: {
      get () {
        return `${this.progress}`
      },
      set (val) {
        const v = Number(val)
        if (!isNaN(v)) {
          this.progress = v < 0 ? 0 : v > 100 ? 100 : v
        }
      }
    },
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
          .map((_, idx) => Number(((Math.random() * idx) + 1).toFixed(1)))
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
.row {
  display: flex;
  flex-direction: row;
}
</style>
