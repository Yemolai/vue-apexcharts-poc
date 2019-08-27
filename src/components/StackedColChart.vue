<template>
  <apex-chart
    type="bar"
    :width="width"
    :series="chartSeries"
    :options="chartOptions"
  />
</template>

<script>
import ApexChart from 'vue-apexcharts'
export default {
  name: 'StackedColChart',
  components: { ApexChart },
  props: {
    percentage: Boolean,
    showMenus: Boolean,
    width: {
      type: String || Number,
      default: '100%'
    },
    data: {
      type: Object,
      default: () => ({})
    }
  },
  data () {
    return {
      chartOptions: {
        chart: {
          toolbar: { show: this.showMenus },
          stacked: true,
          stackType: this.percentage === true ? '100%' : 'normal'
        },
        toolbar: { show: !!this.showMenus },
        grid: { show: false },
        dataLabels: { enabled: true },
        legend: {
          show: true
        }
      }
    }
  },
  computed: {
    chartSeries () {
      return Object.keys(this.data)
        .map(k => ({ name: k, data: this.data[k] }))
    }
  }
}
</script>

<style>

</style>
