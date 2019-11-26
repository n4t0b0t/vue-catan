<template>
  <svg class="chart" />
</template>

<script>
import d3 from "../assets/d3";
export default {
  props: ["data"],
  data() {
    return {
      width: 420,
      barHeight: 20
    };
  },
  mounted() {
    this.generateChart();
  },
  methods: {
    generateChart() {
      const chart = d3
        .select(".chart")
        .attr("width", this.width)
        .attr("height", this.barHeight * this.data.length);

      const bar = chart
        .selectAll("g")
        .data(this.data)
        .enter()
        .append("g")
        .attr("transform", (d, i) => "translate(0," + i * this.barHeight + ")");

      bar
        .append("rect")
        .attr("width", d => this.xScale(d.count))
        .attr("height", this.barHeight - 1);

      bar
        .append("text")
        .attr("x", d => this.xScale(d.count) - 3)
        .attr("y", this.barHeight / 2)
        .attr("dy", ".35em")
        .text(function(d) {
          return d.roll + " rolls: " + d.count;
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
          .selectAll("g")
          .remove();
        this.generateChart();
      },
      deep: true
    }
  }
};
</script>

<style>
.chart rect {
  fill: steelblue;
}

.chart text {
  fill: white;
  font: 10px sans-serif;
  text-anchor: end;
}
</style>
