<template>
  <div>
    <Counter
      v-for="roll in rolls"
      v-bind:key="roll.id"
      v-bind:roll="roll"
      v-on:increase="increaseCount(roll)"
    ></Counter>
    <!-- <button v-on:click="endGame = true">End Game</button>
    <BarChart
      v-if="endGame"
      title="Bar Chart"
      xKey="roll"
      yKey="count"
      :data="rolls"
    /> -->
    <HorizontalChart :data="rolls" />
  </div>
</template>

<script>
import Counter from "../components/Counter.vue";
// import BarChart from "../components/BarChart";
import HorizontalChart from "../components/HorizontalChart";

export default {
  components: {
    Counter,
    // BarChart,
    HorizontalChart
  },
  data() {
    return {
      endGame: false,
      rolls: [
        { id: 1, roll: 1, count: 0 },
        { id: 2, roll: 2, count: 0 },
        { id: 3, roll: 3, count: 0 },
        { id: 4, roll: 4, count: 0 },
        { id: 5, roll: 5, count: 0 },
        { id: 6, roll: 6, count: 0 },
        { id: 7, roll: 7, count: 0 },
        { id: 8, roll: 8, count: 0 },
        { id: 9, roll: 9, count: 0 },
        { id: 10, roll: 10, count: 0 },
        { id: 11, roll: 11, count: 0 },
        { id: 12, roll: 12, count: 0 }
      ]
    };
  },
  methods: {
    increaseCount(roll) {
      roll.count++;
    }
  }
};
</script>
