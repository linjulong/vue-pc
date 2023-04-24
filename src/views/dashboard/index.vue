<template>
  <div class="dashboard-container">
    111
  </div>
</template>

<script>
import { mapGetters } from 'vuex'
export default {
  name: 'Dashboard',
  data() {
    return {
      text: '',
      checked: true,
      text2: '123'
    }
  },
  computed: {
    ...mapGetters(['name'])
  },
  mounted() {
    this.initCharts()
  },
  methods: {
    inputChange(val) {
      console.log('第三方组件事件继承', val)
    },
    initCharts() {
      this.chart = this.$echarts.init(this.$refs.echarts)
      this.setOptions()
      this.chart.on('click', function(params) {
        console.log(params)
      })
    },
    setOptions() {
      this.chart.setOption({
        title: {
          text: 'ECharts 入门示例'
        },
        tooltip: {},
        xAxis: {
          data: ['衬衫', '羊毛衫', '雪纺衫', '裤子', '高跟鞋', '袜子']
        },
        yAxis: {},
        series: [
          {
            name: '销量',
            type: 'bar',
            data: [5, 20, 86, 10, 10, 20]
          }
        ]
      })
    }
  }
}
</script>

<style lang="scss" scoped>
.dashboard {
  &-container {
    margin: 30px;
  }
  &-text {
    font-size: 30px;
    line-height: 46px;
  }
}
#chart {
  width: 600px;
  height: 300px;
}
</style>
