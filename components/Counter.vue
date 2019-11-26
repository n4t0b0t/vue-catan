<template>
  <button v-on:click="$emit('increase')">
    {{ roll.roll }} {{ roll.count }}
  </button>
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
