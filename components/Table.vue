<template>
  <table>
    <tbody>
      <tr>
        <th v-for="header in rowHeaders" v-bind:key="header">{{ header }}</th>
      </tr>
      <tr v-for="roll in rolls" v-bind:key="roll.id">
        <td>{{ roll.number }}</td>
        <td>{{ roll.probability }}</td>
        <td>{{ roll.count }}</td>
        <td>{{ roll.expected }}</td>
        <td><button class="undo-button" v-on:click="$emit('decrease', roll.number)">-</button></td>
      </tr>
    </tbody>
  </table>
</template>

<script>
export default {
  props: ["rolls"],
  data() {
    return {
      rowHeaders: ["Roll", "Probability", "Actual", "Expected"]
    };
  }
};
</script>