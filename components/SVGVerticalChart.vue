<template>
  <svg class="chart" />
</template>

<script>
import d3 from "../assets/d3";
export default {
  props: ["data"],
  data() {
    return {
      width: 360,
      height: 500,
      barWidth: 0
    };
  },
  mounted() {
    this.barWidth = this.width / this.data.length;
    this.generateChart();
  },
  methods: {
    generateChart() {
      const chart = d3
        .select(".chart")
        .attr("width", this.width)
        .attr("height", this.height);

      const bar = chart
        .selectAll("g")
        .data(this.data)
        .enter()
        .append("g")
        .attr("transform", (d, i) => {
          return "translate(" + i * this.barWidth + ",0)";
        });

      bar
        .append("rect")
        .attr("y", d => this.yScale(d.count))
        .attr("height", d => this.height - this.yScale(d.count))
        .attr("width", this.barWidth - 1);

      bar
        .append("text")
        .attr("transform", d => {
          return (
            "translate(" +
            this.barWidth / 2 +
            "," +
            (this.yScale(d.count) + 50) +
            ")rotate(90)"
          );
        })
        .attr("dy", ".75em")
        .attr("anchor", "middle")
        .text(function(d) {
          return d.number + " rolls: " + d.count;
        });

      bar
        .append("line")
        .attr("x1", 0)
        .attr("y1", d => this.yScale(d.expected))
        .attr("x2", this.barWidth - 1)
        .attr("y2", d => this.yScale(d.expected))
        .style("stroke", "white");
    }
  },
  computed: {
    yScale() {
      return d3
        .scaleLinear()
        .domain([0, d3.max(this.data.map(d => d.count))])
        .range([this.height, 0]);
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
