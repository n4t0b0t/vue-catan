<template>
  <div>
    <button class="counter-button" v-on:click="$emit('increase')">{{ roll.roll }}</button>
  </div>
</template>

<script>
export default {
  props: ["roll"]
};
</script>

<style>
.counter-button {
  float: left;
}

button {
  margin-left: 5px;
  font-size: 14px;
  font-weight: bold;
  border-radius: 3px;
  padding: 7px 20px;
  margin: 5px;
  color: #ffffff;
  background-color: #5995da;
}

button:hover {
  background-color: #76aeed;
}

button:active {
  background-color: #407fc7;
}
</style>
