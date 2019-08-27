<template>
  <apex-chart
    type="area"
    :width="width"
    :series="chartSeries"
    :options="chartOptions"
  />
</template>

<script>
import ApexChart from 'vue-apexcharts'

export default {
  name: 'AreaChart',
  components: { ApexChart },
  props: {
    showMenus: Boolean,
    mono: Boolean,
    width: {
      type: String || Number,
      default: '100%'
    },
    color: {
      type: String || Array,
      default: '#15b720'
    },
    data: {
      type: Object,
      default: () => ({}),
      required: true
    }
  },
  computed: {
    chartSeries () {
      return Object.keys(this.data)
        .map(k => ({
          name: k,
          data: this.data[k]
        }))
    }
  },
  data () {
    return {
      chartOptions: {
        chart: {
          toolbar: { show: !!this.showMenus }
        },
        grid: { show: false },
        dataLabels: { enabled: true },
        legend: {
          show: true
        },
        stroke: {
          curve: 'smooth',
          lineCap: 'round',
          width: 1
        },
        theme: {
          palette: 'pallete3',
          monochrome: {
            enabled: this.mono,
            shadeTo: 'dark',
            shadeIntensity: 0.5,
            color: this.color
          }
        },
        xaxis: {
          labels: { show: false },
          axisBorder: { show: false },
          axisTicks: { show: false }
        },
        yaxis: {
          axisBorder: { show: false },
          axisTicks: { show: false }
        }
      }
    }
  }
}
</script>

<style>
.card {
  margin: 0.5em;
  border-radius: 0.1em;
}
</style>
