<script setup>
import { computed, ref, provide } from "vue";
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
} from "echarts/components";
import VChart, { THEME_KEY } from 'vue-echarts';
import { use } from "echarts/core";

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

provide(THEME_KEY, 'dark');

let isLoading = ref(true);
let q = ref(-1);
let dataset = ref({
    "Q1-2023": {
        dates: ["2023-01", "2023-02", "2023-03"],
        data: [10, 6, 7]
    },
    "Q2-2023": {
        dates: ["2023-04", "2023-05"],
        data: [3, 2]
    }
})
let quarters = ref(["Q1-2023", "Q2-2023"])

let chartOptions = computed(() => {
    let currentIndex = q.value === -1 ? quarters.value.length - 1 : q.value
    console.log(dataset.value[quarters.value[currentIndex]].dates)
    let option = {
        baseOption: {
            title: {
                text: "Numbers for year 2023",
            },
            xAxis: {
                type: "category",
                name: "Dates",
                data: dataset.value[quarters.value[currentIndex]].dates,
            },
            yAxis: {
                type: "",
                name: "Numbers",
                min: 0,
            },
            timeline: {
                axisType: "category",
                show: true,
                data: quarters.value,
                replaceMerge: "series",
                currentIndex: currentIndex
            }
        },
        options: []
    }
    quarters.value.forEach((quarter) => {
        option.options.push({
            series: [
                {
                    name: "number",
                    type: "line",
                    symbolSize: 8,
                    data: dataset.value[quarter].data
                }
            ]
        })
    })
    console.log(option)
    isLoading.value = false;
    return option;
})
</script>

<template>
    <v-chart :option="chartOptions" class="chart" autoresize></v-chart>
</template>
<style scoped>
.chart {
    height: 80vh;
    width: 110vh;
}
</style>