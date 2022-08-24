<template>
  <v-app>
    <v-main>
      <v-card color="basil">
        <v-card-title class="text-center justify-center py-6">
          <v-row no-gutters>
            <v-col cols="10">
              <h1 class="font-weight-bold text-h2 basil--text">
                {{stats[currentDataIndex].title}}
              </h1>
            </v-col>
            <v-col cols="2">
              <v-select
                v-model="menuValue"
                :items="stats"
                item-value="value"
                item-text="title"
                label="統計資料"
                outlined
                @change="changeData(menuValue)"
              ></v-select>
            </v-col>
          </v-row>
        </v-card-title>

        <v-tabs
          v-model="tab"
          background-color="transparent"
          color="basil"
          grow
        >
          <v-tab
            v-for="item in stats[currentDataIndex].charts"
            :key="item.id"
          >
            {{ item.title }}
          </v-tab>
        </v-tabs>

        <v-tabs-items v-model="tab">
          <v-tab-item
            v-for="item in stats[currentDataIndex].charts"
            :key="item.id"
          >
            <v-card
              color="basil"
              flat
            >
              <!-- BarChart -->
              <v-card-text v-if="item.type=='bar'">
                <v-row no-gutters>
                  <v-col cols="12">
                    <BarChart
                      :data="stats[currentDataIndex].data"
                      :options="chartOptions.bar"
                      :chartId="item.id"
                      :height="config.height"
                    />
                  </v-col>
                </v-row>
              </v-card-text>
              <!-- radar -->
              <v-card-text v-else-if="item.type=='radar'">
                <v-row no-gutters>
                  <v-col cols="12">
                    <RadarChart
                      :data="stats[currentDataIndex].data"
                      :options="chartOptions.radar"
                      :chartId="item.id"
                      :height="config.height"
                    />
                  </v-col>
                </v-row>
              </v-card-text>
              <!-- bubble -->
              <v-card-text v-else-if="item.type=='bubble'">
                <v-row no-gutters>
                  <v-col cols="12">
                    <BubbleChart
                      :data="stats[currentDataIndex].data"
                      :options="chartOptions.bubble"
                      :chartId="item.id"
                      :height="config.height"
                    />
                  </v-col>
                </v-row>
              </v-card-text>
              <!-- Doughnut -->
              <v-card-text v-else-if="item.type=='doughnut'">
                <v-row no-gutters>
                  <v-col cols="12">
                    <DoughnutChart
                      :data="stats[currentDataIndex].data"
                      :chartId="item.id"
                      :height="config.height"
                    />
                  </v-col>
                </v-row>
              </v-card-text>
              <!-- Line Chart -->
              <v-card-text v-else-if="item.type=='line'">
                <v-row no-gutters>
                  <v-col cols="12">
                    <LineChart
                      :data="stats[currentDataIndex].data"
                      :options="chartOptions.line"
                      :chartId="item.id"
                      :height="config.height"
                    />
                  </v-col>
                </v-row>
              </v-card-text>
              <!-- Pie Chart -->
              <v-card-text v-else-if="item.type=='pie'">
                <v-row no-gutters>
                  <v-col cols="12">
                    <PieChart
                      :data="stats[currentDataIndex].data"
                      :options="chartOptions.line"
                      :chartId="item.id"
                      :height="config.height"
                    />
                  </v-col>
                </v-row>
              </v-card-text>
            </v-card>
          </v-tab-item>
        </v-tabs-items>

      </v-card>

    </v-main>
  </v-app>

</template>

<script>
// component
import LineChart from "./components/LineChart.vue";
import BarChart from "./components/BarChart.vue";
import RadarChart from "./components/RadarChart.vue";
import BubbleChart from "./components/BubbleChart.vue";
import DoughnutChart from "./components/DoughnutChart.vue";
import PieChart from "./components/PieChart.vue";

// Data
import SChartData from "@/assets/JSON/salaryChartData.json";
import JChartData from "@/assets/JSON/jobChartData.json";
import PChartData from "@/assets/JSON/peoplesChartData.json";
import AChartData from "@/assets/JSON/acChartData.json";

export default {
  data() {
    return {
      tab: null,

      stats: [
        {
          title: "110年每人每月經常性薪資",
          value: 0,
          charts: [
            { title: "Bar Chart", type: "bar", id: "0" },
            { title: "Line Chart", type: "line", id: "1" },
            { title: "Radar Chart", type: "radar", id: "2" },
          ],
          data: SChartData,
        },
        {
          title: "101年及110年就業者行業結構比較",
          value: 1,
          charts: [
            { title: "Bar Chart", type: "bar", id: "3" },
            { title: "Line Chart", type: "line", id: "4" },
            { title: "Radar Chart", type: "radar", id: "5" },
          ],
          data: JChartData,
        },
        {
          title: "2022 7月出口貨物價值",
          value: 2,
          charts: [{ title: "Bubble Chart", type: "bubble", id: "6" }],
          data: PChartData,
        },
        {
          title: "2021年 發電量",
          value: 3,
          charts: [
            { title: "Doughnut Chart", type: "doughnut", id: "7" },
            { title: "Pie Chart", type: "pie", id: "8" },
          ],
          data: AChartData,
        },
      ],
      menuValue: 0,
      items: [
        { title: "Bar Chart", type: "bar", id: "0" },
        { title: "Bubble Chart", type: "bubble", id: "1" },
        { title: "Doughnut Chart", type: "doughnut", id: "2" },
        { title: "Line Chart", type: "line", id: "3" },
        { title: "Radar Chart", type: "radar", id: "4" },
      ],
      chartData: {},
      chartOptions: {
        bar: {
          responsive: true,
          //width & height setting
          maintainAspectRatio: false,
        },
        bubble: {
          responsive: true,
          //width & height setting
          maintainAspectRatio: false,
        },
        doughnut: {
          responsive: true,
          //width & height setting
          maintainAspectRatio: false,
        },
        line: {
          responsive: true,
          //width & height setting
          maintainAspectRatio: false,
        },
        radar: {
          responsive: true,
          //width & height setting
          maintainAspectRatio: false,
        },
      },

      config: {
        height: 700,
        width: 100,
      },
    };
  },
  components: {
    LineChart,
    BarChart,
    RadarChart,
    BubbleChart,
    DoughnutChart,
    PieChart
  },
  created() {
    const self = this;

    let peoples = PChartData;
    peoples.datasets.forEach((element) => {
      let rndColor = Math.floor(Math.random() * 16777215).toString(16);
      element.backgroundColor = "#" + rndColor;
      element.data.forEach((item) => {
        item.r /= 250;
      });
    });
    self.stats[2].data = peoples;

    self.changeData(self.menuValue);
  },
  mounted() {},
  methods: {
    changeData: function (value) {
      const self = this;
      if (value == 0) self.chartData = SChartData;
      else self.chartData = JChartData;
    },
  },
  computed: {
    currentDataIndex: function () {
      const self = this;
      const index = self.stats.findIndex(
        (item) => item.value == self.menuValue
      );
      return index;
    },
  },
};
</script>

<style>
.basil {
  background-color: #fffbe6 !important;
}
.basil--text {
  color: #356859 !important;
}
</style>