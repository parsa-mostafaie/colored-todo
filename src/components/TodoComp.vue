<template>
  <div class="todo" :style="{ backgroundColor: bgc, width: '100%' }">
    <span><slot></slot></span
    ><span class="close" @click="emit('remove')">x</span>
  </div>
</template>
<script setup>
import { defineProps, reactive, defineEmits } from "vue";

let props = defineProps(["bgcolor"]);

let emit = defineEmits(["remove"]);

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
