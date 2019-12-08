<template>
  <div>
    <button v-on:click="rollDice, $emit()">Roll Dice!</button>
    <div>Result: {{ this.die1 }} + {{ this.die2 }} = {{ this.diceTotal }}</div>
  </div>
</template>

<script>
export default {
    data() {
        return {
            die1: 0,
            die2: 0
        }
    },
    methods: {
        rollDice() {
            this.die1 = Math.floor(Math.random() * 6) + 1
            this.die2 = Math.floor(Math.random() * 6) + 1
        }
    },
    computed: {
        diceTotal() {
            return this.die1 + this.die2
        }
    }
};
</script>