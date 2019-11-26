<template>
  <button v-on:click="$emit('increase')">{{ roll.roll }}</button>
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
</style>
