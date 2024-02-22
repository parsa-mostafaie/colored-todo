<template>
  <div></div>
</template>
<style scoped>
div {
  --color: v-bind("bgc");
  background: var(--color);
  border-radius: 100%;
  height: 1rem;
  aspect-ratio: 1;
  border: 1px solid #929292;
}
</style>
<script setup>
import { defineProps } from "vue";

let props = defineProps(["bgcolor"]);

let bgc = props.bgcolor || "#000";
</script>
