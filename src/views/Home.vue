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
        xAxis: {
          data: ["Mon", "Tue", "Wed", "Thu", "Fri", "Sat", "Sun"],
          boundaryGap: false,
          axisTick: {
            show: false
          }
        },
        grid: {
          left: 10,
          right: 10,
          bottom: 20,
          top: 30,
          containLabel: true
        },
        tooltip: {
          trigger: "axis",
          axisPointer: {
            type: "cross"
          },
          padding: [5, 10]
        },
        yAxis: {
          axisTick: {
            show: false
          }
        },
        legend: {
          data: ["expected", "actual"]
        },
        series: [
          {
            name: "expected",
            itemStyle: {
              normal: {
                color: "#FF005A",
                lineStyle: {
                  color: "#FF005A",
                  width: 2
                }
              }
            },
            smooth: true,
            type: "line",
            data: [100, 120, 161, 134, 105, 160, 165],
            animationDuration: 2800,
            animationEasing: "cubicInOut"
          },
          {
            name: "actual",
            smooth: true,
            type: "line",
            itemStyle: {
              normal: {
                color: "#3888fa",
                lineStyle: {
                  color: "#3888fa",
                  width: 2
                },
                areaStyle: {
                  color: "#f3f8ff"
                }
              }
            },
            data: [120, 82, 91, 154, 162, 140, 145],
            animationDuration: 2800,
            animationEasing: "quadraticOut"
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
