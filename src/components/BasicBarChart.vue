<template>
  <apex-chart
    type="bar"
    :width="width"
    :options="chartOptions"
    :series="chartSeries"
  />
</template>

<script>
import ApexChart from 'vue-apexcharts'

export default {
  name: 'BasicBarChart',
  components: { ApexChart },
  props: {
    width: {
      type: String || Number,
      default: '100%'
    },
    options: {
      type: Object,
      default: () => ({})
    },
    xAxis: {
      type: Object,
      default: () => ({})
    },
    data: {
      type: Object,
      default: () => ({})
    }
  },
  computed: {
    chartOptions () {
      return {
        xaxis: this.xAxis
      }
    },
    chartSeries () {
      return Object.keys(this.data).map(k => ({ name: k, data: this.data[k] }))
    }
  }
}
</script>
