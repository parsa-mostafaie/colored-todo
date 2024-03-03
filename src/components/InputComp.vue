<script setup>
import { defineModel, defineProps, reactive } from "vue";

let props = defineProps(["placeholder", "bgcolor"]);

let placeholder = reactive(props.placeholder);
let bgc = reactive(props.bgcolor);

const [txt_model, modifiers] = defineModel({
  set(value) {
    if (modifiers.trim) {
      return value.trim();
    }
    return value;
  },
});
</script>

<template>
  <div style="width: 100%">
    <input
      v-model="txt_model"
      style="width: 100%"
      :placeholder="placeholder"
      :style="{ backgroundColor: bgc }"
    />
  </div>
</template>

<style scoped>
input {
  box-sizing: border-box;
  padding: 10px;
  border-radius: 5px;
  border: 1px solid black;
  outline: 0px solid #0f05;
  transition: 100ms linear;
}
input:focus {
  outline-width: 5px;
}
</style>
