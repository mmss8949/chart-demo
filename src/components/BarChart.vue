<template>

  <Bar
    :chart-options="options"
    :chart-data="chartData"
    :chart-id="chartId"
    :dataset-id-key="datasetIdKey"
    :plugins="plugins"
    :css-classes="cssClasses"
    :styles="styles"
    :width="width"
    :height="height"
  />

</template>

<script>
import { Bar } from "vue-chartjs/legacy";
import Chart from "chart.js/auto";

export default {
  name: "BarChart",
  components: { Bar },
  props: {
    data: {
      type: Object,
    },
    chartId: {
      type: String,
      default: "bar-chart",
    },
    datasetIdKey: {
      type: String,
      default: "label",
    },
    width: {
      type: Number,
      default: 400,
    },
    height: {
      type: Number,
      default: 700,
    },
    cssClasses: {
      default: "",
      type: String,
    },
    styles: {
      type: Object,
      default: () => {},
    },
    plugins: {
      type: Array,
      default: () => [],
    },
  },

  computed: {
    chartData() {
      const self = this;
      return self.data; /* mutable chart data */
    },
  },
    data() {
    return {
      options: {
        responsive: true,
        //width & height setting
        maintainAspectRatio: false,
      },
    };
  },
};
</script>