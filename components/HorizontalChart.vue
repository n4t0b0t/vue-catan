<template>
  <div class="chart"></div>
</template>

<script>
import * as d3 from "d3-selection";
export default {
  props: ["data"],
  //   computed: {
  //     chartData: function() {
  //       return this.data;
  //     }
  //   },
  mounted() {
    this.generateChart();
    console.log("I AM MOUNTED!");
  },
  methods: {
    generateChart() {
      d3.select(".chart")
        .selectAll("div")
        .data(this.data)
        .enter()
        .append("div")
        .style("width", function(d) {
          return d.count * 10 + "px";
        })
        .text(function(d) {
          return d.roll;
        });
    }
  },
  watch: {
    data: {
      handler: function(val) {
        d3.select(".chart")
          .selectAll("div")
          .remove();
        this.generateChart();
      },
      deep: true
    }
  }
};
</script>

<style>
.chart div {
  font: 10px sans-serif;
  background-color: steelblue;
  text-align: right;
  padding: 3px;
  margin: 1px;
  color: white;
}
</style>
