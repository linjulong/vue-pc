<template>
  <div class="dashboard-container">
    <svg-icon icon-class="username"></svg-icon>
    <div class="dashboard-text">name: {{ name }}</div>
    <div ref="echarts" id="chart"></div>
    <h3>自定义input</h3>
    {{text}}
    <my-input :value="text" @input="text = $event" />
    <my-input v-model="text" />
    <!-- v-model语法糖自己变成:value="text" @input="text = $event" -->
    <h3>自定义CheckBox</h3>
    {{checked}}
    <my-checkbox @change="checked = $event" :checked="checked" />
    <my-checkbox v-model="checked" />

    <h3>第三方input</h3>
    {{text2}}

    <debounce events="input" :wait="250">
      <!-- <input @input="inputChange" placeholder="输入关键字进行搜索" /> -->
      <el-input v-model="text2" @input="inputChange" />
      <!-- <my-el-input suffix-icon="el-icon-date" v-model="text2" @input="inputChange" @input.native="inputChange" /> -->
    </debounce>
  </div>
</template>

<script>
import { mapGetters } from "vuex";
import myInput from "@/components/Input/index";
import myCheckbox from "@/components/Checkbox/index";
import myElInput from "@/components/ElInput/index";
export default {
  name: "Dashboard",
  components: {
    myInput, myCheckbox, myElInput
  },
  data () {
    return {
      text: '',
      checked: true,
      text2: '123'
    }
  },
  computed: {
    ...mapGetters(["name"])
  },
  mounted () {
    this.initCharts();
  },
  methods: {
    inputChange (val) {
      console.log('第三方组件事件继承', val)
    },
    initCharts () {
      this.chart = this.$echarts.init(this.$refs.echarts);
      this.setOptions();
      this.chart.on("click", function (params) {
        console.log(params);
      });
    },
    setOptions () {
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
