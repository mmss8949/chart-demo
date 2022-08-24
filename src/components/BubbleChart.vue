<template>

  <Bubble
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
import { Bubble } from "vue-chartjs/legacy";
import Chart from "chart.js/auto";

export default {
  name: "BubbleChart",
  components: { Bubble },

  props: {
    data: {
      type: Object,
    },
    chartId: {
      type: String,
      default: "bubble-chart",
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

        scales: {
          x: {
            title: {
              display: true,
              text: "上年同月出口值(百萬美元)",
            },
            // ticks: {
            //   // Include a dollar sign in the ticks
            //   callback: function (value, index, ticks) {
            //     return "$" + value;
            //   },
            // },
          },
          y: {
            title: {
              display: true,
              text: "年增率%",
            },
            // ticks: {
            //   // Include a dollar sign in the ticks
            //   callback: function (value, index, ticks) {
            //     return "$" + value;
            //   },
            // },
          },
        },
        plugins: {
          tooltip: {
            callbacks: {
              label: function (context) {
                let label = context.dataset.label || "";

                if (label) {
                  label += ": (";
                }
                if (context.parsed.x !== null) {
                  label += new Intl.NumberFormat("en-US", {
                    maximumFractionDigits: 3,
                  }).format(context.parsed.x);
                  label += ",  ";
                }
                if (context.parsed.y !== null) {
                  label +=
                    new Intl.NumberFormat("en-US", {
                      maximumFractionDigits: 0,
                    }).format(context.parsed.y) + "%";
                  label += ",  ";
                }
                if (context.parsed._custom !== null) {
                  label += new Intl.NumberFormat("en-US", {
                    maximumFractionDigits: 3,
                  }).format(context.parsed._custom*250);
                }
                if (label) {
                  label += " )";
                }
                return label;
              },
            },
          },
        },
      },
    };
  },
};
</script>