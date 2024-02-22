<template>
  <button><slot>Click</slot></button>
</template>
<style scoped>
button {
  --btn-color: v-bind("bgc");
  padding: 10px;
  color: white;
  border-radius: 5px;
  border: none;
  outline: none;
  border: 1px solid var(--btn-color);
  background-color: var(--btn-color);
}
button:hover {
  color: var(--btn-color);
  background-color: white;
}
</style>
<script setup>
import { defineProps } from "vue";

let props = defineProps(["bgcolor"]);

let colors = { danger: "#dc3545", info: "#17a2b8" };

let bgc = colors[props.bgcolor] || "#dc3545";
</script>
