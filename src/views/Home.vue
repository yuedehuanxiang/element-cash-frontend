<template>
  <div class="home">
    <div class="container">
      <github-corner style="position: absolute; top: 0px; border: 0; right: 0;"></github-corner>
      <panel-group></panel-group>
      <div style="width: 100%; height: 500px;" ref="chart"></div>
    </div>
  </div>
</template>

<script>
import GithubCorner from "@/components/GithubCorner";
import PanelGroup from "@/components/PanelGroup";
import echarts from "echarts";
require("echarts/theme/macarons");
export default {
  components: {
    GithubCorner,
    PanelGroup
  },
  methods: {
    initChart() {
      const myChart = echarts.init(this.$refs.chart, "macarons");
      const option = {
        title: { text: "销售额" },
        tooltip: {},
        legend: { data: ["销量"] },
        xAxis: {
          data: ["衬衫", "羊毛衫", "雪纺衫", "裤子", "高跟鞋", "袜子"]
        },
        yAxis: {},
        series: [
          {
            name: "销量",
            type: "bar",
            data: [5, 20, 36, 10, 10, 20]
          }
        ]
      };
      myChart.setOption(option);
    }
  },
  mounted() {
    this.initChart();
  }
};
</script>

<style scoped>
.home {
  width: 100%;
  height: 100%;
  background-color: rgb(240, 242, 245);
}
.container {
  padding: 32px;
}
</style>
