<template>
  <div class="counter-button">
    {{ roll.roll }}
    <button v-on:click="$emit('increase')">+</button>
    <button v-on:click="$emit('decrease')">-</button>
  </div>
</template>

<script>
export default {
  props: ["roll"]
};
</script>

<style>
button {
  padding: 10px;
}
.counter-button {
  float: left;
  margin: 10px;
  padding: 0 10px;
  border: 1px solid white;
  font-size: 1rem;
}
</style>
