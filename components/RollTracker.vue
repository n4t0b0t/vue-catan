<template>
  <div>
    <Dice v-if="!manual" />
    <Counter
      v-for="roll in rolls"
      v-bind:key="roll.id"
      v-bind:roll="roll"
      v-on:increase="increaseCount(roll)"
      v-on:decrease="decreaseCount(roll)"
    ></Counter>
    <button class="undo-button" v-on:click="undoLastRoll">Undo</button>
    <Table :rolls="rolls" v-on:decrease="decreaseCount" />
    <SVGVerticalChart :data="rolls" />
    <!-- <VerticalChart
      v-if="endGame"
      title="Bar Chart"
      xKey="roll"
      yKey="count"
      :data="rolls"
    />-->
  </div>
</template>

<script>
import Dice from "../components/Dice.vue";
import Counter from "../components/Counter.vue";
import SVGVerticalChart from "../components/SVGVerticalChart";
import Table from "../components/Table";

export default {
  components: {
    Dice,
    Counter,
    SVGVerticalChart,
    Table
  },
  props: { manual: Boolean },
  data() {
    return {
      totalRolls: 0,
      rolls: [
        { id: 2, roll: 2, count: 0, expected: 0, probability: 0.028 },
        { id: 3, roll: 3, count: 0, expected: 0, probability: 0.056 },
        { id: 4, roll: 4, count: 0, expected: 0, probability: 0.083 },
        { id: 5, roll: 5, count: 0, expected: 0, probability: 0.111 },
        { id: 6, roll: 6, count: 0, expected: 0, probability: 0.139 },
        { id: 7, roll: 7, count: 0, expected: 0, probability: 0.167 },
        { id: 8, roll: 8, count: 0, expected: 0, probability: 0.139 },
        { id: 9, roll: 9, count: 0, expected: 0, probability: 0.111 },
        { id: 10, roll: 10, count: 0, expected: 0, probability: 0.083 },
        { id: 11, roll: 11, count: 0, expected: 0, probability: 0.056 },
        { id: 12, roll: 12, count: 0, expected: 0, probability: 0.028 }
      ],
      lastRoll: 0
    };
  },
  methods: {
    increaseCount(roll) {
      this.totalRolls++;
      roll.count++;
      this.lastRoll = roll;
      this.calculateExpectedRolls();
    },
    decreaseCount(roll) {
      if (roll.count > 0) {
        this.totalRolls--;
        roll.count--;
        this.lastRoll = 0;
        this.calculateExpectedRolls();
      }
    },
    undoLastRoll() {
      if (!this.lastRoll) {
        alert("no roll to undo");
      } else {
        this.decreaseCount(this.lastRoll);
        this.calculateExpectedRolls();
      }
    },
    calculateExpectedRolls() {
      for (const roll of this.rolls) {
        roll.expected =
          Math.round(this.totalRolls * roll.probability * 1000) / 1000;
      }
    }
  }
};
</script>

<style>
.undo-button {
  margin-left: 5px;
  font-size: 14px;
  font-weight: bold;
  border-radius: 3px;
  padding: 7px 20px;
  margin: 5px;
  color: #ffffff;
  background-color: #da595f;
}

.undo-button:hover {
  background-color: #ed7676;
}

.undo-button:active {
  background-color: #c74052;
}
</style>