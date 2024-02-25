<template>
  <div
    class="todo"
    @click.self="emit('stChange')"
    :style="{
      backgroundColor: bgc,
      width: '100%',
      filter: `brightness(${st ? '90' : '100'}%)`,
    }"
  >
    <span
      :style="{
        textDecoration: (st && 'line-through') || 'unset',
      }"
    >
      <slot></slot> </span
    ><span class="close" @click="emit('remove')">x</span>
  </div>
</template>
<script setup>
import { defineProps, reactive, defineEmits } from "vue";

let props = defineProps(["bgcolor", "st"]);

let emit = defineEmits(["remove", "stChange"]);

let st = reactive(props.st);

let bgc = reactive(props.bgcolor);
</script>
<style scoped>
.todo {
  user-select: none;
  box-sizing: border-box;
  padding: 10px;
  border-radius: 5px;
  border: 1px solid #929292;
  display: flex;
  justify-content: space-between;
  align-items: center;
}

.close {
  color: #bbb;
  vertical-align: middle;
}
</style>
