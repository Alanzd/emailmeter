<template>
    <apexchart type="bar" height="350" :options="chartOptions" :series="series"></apexchart>
</template>

<script>
import VueApexCharts from 'vue3-apexcharts'
export default {
  name: 'UserDetails',
  data(){
    return {
      series: [{
        data: []
      }],
      chartOptions: {
        chart: {
          type: 'bar',
          height: 350
        },
        plotOptions: {
          bar: {
            borderRadius: 4,
            horizontal: true,
          }
        },
        dataLabels: {
          enabled: false
        },
        xaxis: {
          categories: [],
        }
      }
    }
  },
  props: {
    // index: Number,
    user: Object,
  },
  components: {
    apexchart: VueApexCharts
  }
}
</script>
