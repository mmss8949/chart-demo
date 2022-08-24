<template>

  <Pie
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
import { Pie } from "vue-chartjs/legacy";
import Chart from "chart.js/auto";

export default {
  name: "LineChart",
  components: { Pie },

  props: {
    data: {
      type: Object,
    },
    chartId: {
      type: String,
      default: "line-chart",
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
  mounted() {},
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