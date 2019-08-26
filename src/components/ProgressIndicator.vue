<template>
  <apex-chart
    :width="width"
    type="radialBar"
    :options="chartOptions"
    :series="chartData"/>
</template>

<script>
import ApexChart from 'vue-apexcharts'

export default {
  name: 'ProgressIndicator',
  components: { ApexChart },
  props: {
    startAt: {
      type: String,
      enum: ['top', 'left', 'right', 'bottom'],
      default: 'left'
    },
    mode: {
      type: String,
      enum: ['half', 'full'],
      default: 'full'
    },
    width: {
      type: String || Number,
      default: '100%'
    },
    scale: {
      type: Number,
      default: 1
    },
    options: {
      type: Object,
      default: () => ({})
    },
    name: {
      type: String,
      default: 'Value'
    },
    value: {
      type: Number,
      default: 0
    },
    nameColor: String,
    valueColor: String,
    textColor: String,
    hideMenus: Boolean
  },
  computed: {
    chartOptions () {
      const starts = { left: -90, top: 0, right: 90, bottom: 180 }
      const startAngle = starts[this.startAt]
      const endAngle = startAngle + (this.mode === 'full' ? 360 : 180)
      return {
        plotOptions: {
          radialBar: {
            startAngle,
            endAngle,
            track: {
              background: '#e7e7e7',
              strokeWidth: '97%',
              margin: 5, // margin is in pixels
              shadow: {
                enabled: true,
                top: 2,
                left: 0,
                color: '#999',
                opacity: 1,
                blur: 2
              }
            },
            dataLabels: {
              name: {
                show: false
              },
              value: {
                offsetY: 10,
                fontSize: '1.4em',
                formatter: () => `${this.value.toLocaleString()}%`
              }
            }
          }
        },
        fill: {
          type: 'gradient',
          gradient: {
            shade: 'light',
            shadeIntensity: 0.4,
            inverseColors: false,
            opacityFrom: 1,
            opacityTo: 1,
            stops: [0, 50, 53, 91]
          }
        },
        labels: [this.name]
      }
    },
    chartData () {
      const first = this.value < 0 ? 0 : this.value
      // const second = this.value > 100 ? 0 : 100 - this.value
      return [first]
    }
  }
}
</script>

<style>
.flex {
  display: flex
}
.flex .flex-center {
  justify-content: center;
  justify-items: center;
}
.flex .column {
  flex-direction: column;
}
.text-name {
  font-size: 1.4em;
}
</style>
