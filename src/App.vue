<script setup>
import { use } from 'echarts/core';
import { CanvasRenderer } from 'echarts/renderers';
import { LineChart } from 'echarts/charts';
import {
  DataZoomInsideComponent,
  DataZoomSliderComponent,
  GridComponent,
  TooltipComponent,
  TimelineComponent,
  VisualMapComponent,
  MarkLineComponent,
  PolarComponent,
  TitleComponent,
  LegendComponent,
} from 'echarts/components';
import VChart from 'vue-echarts';
import { ref } from 'vue';

use([
  LineChart,
  CanvasRenderer,
  DataZoomInsideComponent,
  DataZoomSliderComponent,
  GridComponent,
  MarkLineComponent,
  PolarComponent,
  TooltipComponent,
  TimelineComponent,
  VisualMapComponent,
  TitleComponent,
  LegendComponent,
]);

const option = ref({
  baseOption: {
    title: {
      text: "Issues for year 2023",
      left: "10%",
    },
    legend: {
      data: ["nb_resolved", "nb_submitted"],
      formatter: (name) => {
        let msg = "";
        if (name === "nb_resolved") {
          msg = "Resolved";
        } else if (name === "nb_submitted") {
          msg = "Submitted";
        }
        return msg + " issues";
      },
      top: "2%",
      right: "5%",
    },
    tooltip: {
      trigger: "axis",
    },
    xAxis: {
      type: "category",
      name: "Dates",
    },
    yAxis: {
      type: "",
      name: "Number of issues",
      min: 0,
    },
    timeline: {
      axisType: "category",
      show: true,
      data: ["Q1-2023", "Q2-2023"],
    },
    series: [
      {
        name: "nb_resolved",
        type: "line",
        color: "green",
        dimensions: ["dates", "nb_resolved"],
        symbolSize: 8,
      },
      // {
      //   name: "nb_submitted",
      //   type: "line",
      //   color: "red",
      //   dimensions: ["dates", "nb_submitted"],
      //   symbolSize: 8,
      // },
    ],
  },
  options: [
    {
      dataset: {
        source: [
          {
            quarter: "Q1-2023",
            nb_resolved: 10,
            nb_submitted: 8,
            dates: "2023-01",
          },
          {
            quarter: "Q1-2023",
            nb_resolved: 16,
            nb_submitted: 15,
            dates: "2023-02",
          },
          {
            quarter: "Q1-2023",
            nb_resolved: 28,
            nb_submitted: 19,
            dates: "2023-03",
          },
        ],
      },
    },
    {
      dataset: {
        source: [
          {
            quarter: "Q2-2023",
            nb_resolved: 3,
            nb_submitted: 4,
            dates: "2023-04",
          },
          {
            quarter: "Q2-2023",
            nb_resolved: 5,
            nb_submitted: 9,
            dates: "2023-05",
          },
        ],
      },
    },
  ],
});
</script>

<template>
  <div class="common-layout">
    <el-container>
      <el-main>
        <el-row class="el-row" :gutter="12">
          <el-col :span="24">
            <el-card class="no-v-padding">
              <v-chart :option="option" class="chart" autoresize></v-chart>
            </el-card>
          </el-col>
        </el-row>
      </el-main>
    </el-container>
  </div>
</template>

<style scoped>
.no-v-padding {
  padding-right: 0;
  padding-left: 0;
}

.el-row {
  margin-bottom: 10px;
}

.chart {
  height: 80vh;
  width: 110vh;
}
</style>
