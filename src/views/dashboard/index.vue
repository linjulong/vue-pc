<template>
  <div class="dashboard-container">
    <svg-icon icon-class="username"></svg-icon>
    <div class="dashboard-text">name: {{ name }}</div>
    <div ref="echarts" id="chart"></div>
  </div>
</template>

<script>
import { mapGetters } from "vuex";

export default {
  name: "Dashboard",
  computed: {
    ...mapGetters(["name"])
  },
  mounted() {
    this.initCharts();
  },
  methods: {
    initCharts() {
      this.chart = this.$echarts.init(this.$refs.echarts);
      this.setOptions();
      this.chart.on("click", function(params) {
        console.log(params);
      });
    },
    setOptions() {
      this.chart.setOption({
        title: {
          text: "ECharts 入门示例"
        },
        tooltip: {},
        xAxis: {
          data: ["衬衫", "羊毛衫", "雪纺衫", "裤子", "高跟鞋", "袜子"]
        },
        yAxis: {},
        series: [
          {
            name: "销量",
            type: "bar",
            data: [5, 20, 86, 10, 10, 20]
          }
        ]
      });
    }
  }
};
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
