<template>
  <div class="chart"></div>
</template>

<script>
import d3 from "../assets/d3";
export default {
  props: ["data"],
  //   computed: {
  //     chartData: function() {
  //       return this.data;
  //     }
  //   },
  mounted() {
    this.generateChart();
  },
  methods: {
    generateChart() {
      console.log(d3.max(this.data.map(d => d.count)));
      //   var x = d3
      //     .scaleLinear([0, d3.max(this.data.map(d => d.count))])
      //     .range([0, 420]);
      return d3
        .select(".chart")
        .selectAll("div")
        .data(this.data)
        .enter()
        .append("div")
        .style("width", d => this.xScale(d.count) + "px")
        .text(function(d) {
          return d.roll;
        });
    }
  },
  computed: {
    xScale() {
      return d3
        .scaleLinear()
        .domain([0, d3.max(this.data.map(d => d.count))])
        .range([0, 420]);
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
