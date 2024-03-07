<template>
  <header>
    <Container>
      <h1 style="text-align: center">Colored Todo List</h1>
    </Container>
  </header>
  <main>
    <Container>
      <div class="mb-1">
        <Input
          v-model.trim="inp_text"
          placeholder="Type Something Here."
          ref="inp_el"
          :bgcolor="color_comp"
        />
      </div>
      <div class="flex jc-between auto-col mb-1">
        <div class="flex ai-center gap jc-center">
          <ColorSelect
            :bgcolor="color"
            v-for="color in colors"
            @click="changeColor(color)"
            :key="color"
          ></ColorSelect>
        </div>
        <div class="flex gap ai-center jc-center">
          <ButtonComp bgcolor="info" @click="newTodo()">Add</ButtonComp>
          <ButtonComp bgcolor="danger" @click="clearInput()">Clear</ButtonComp>
          <input type="checkbox" id="cb" v-model="searchIn" />
          <label for="cb">Search</label>
        </div>
      </div>
      <hr />
      <div class="todo-container gap-v">
        <TodoComp
          v-for="[index, todo] of todos.entries()"
          :bgcolor="todo.color"
          :key="todo"
          @remove="todos.splice(todos.indexOf(todo), 1)"
          @stChange="changeState(todo)"
          @dragstart="
            (event) => event.dataTransfer.setData('drop_target', index)
          "
          @drop="
            (event) =>
              moveTodo(event.dataTransfer.getData('drop_target'), index)
          "
          :st="computed(() => todo.state)"
          >{{ todo.title }}</TodoComp
        >
      </div>
      <hr v-if="results.length" />
      {{ results.length }} Results Found
      <hr />
    </Container>
  </main>
</template>

<script setup>
import Container from "./components/ContainerComp.vue";
import Input from "./components/InputComp.vue";
import ButtonComp from "./components/ButtonComp.vue";
import ColorSelect from "./components/ColorSelect.vue";
import TodoComp from "./components/TodoComp.vue";

import { ref, computed, reactive, watch } from "vue";

let inp_text = ref("");
let searchIn = ref(false);

let color_s = ref("#fff");

let color_comp = computed(() => color_s);

let results = computed(() =>
  todos.filter((todo) => !searchIn.value || todo.title.includes(inp_text.value))
);

let colors = [
  "#fff",
  "#ffd37f",
  "#fffa81",
  "#d5fa80",
  "#78f87f",
  "#79fbd6",
  "#79fdfe",
  "#7ad6fd",
  "#7b84fc",
  "#d687fc",
  "#ff89fd",
];

function clearInput() {
  inp_text.value = "";
  changeColor("#fff");
  searchIn.value = false;
}

function changeColor(c) {
  color_s.value = c;
}

function newTodo() {
  let ttl = inp_text.value.trim();
  if (ttl) {
    todos.push({
      title: ttl,
      color: color_s.value,
      state: false,
    });
    clearInput();
  }
}

function changeState(td) {
  td.state = !td.state;
}

let _todos_temp_;

try {
  _todos_temp_ = JSON.parse(localStorage.getItem("colored_todos")) || [];
} catch (err) {
  ("nop");
}

_todos_temp_ = Array.isArray(_todos_temp_) ? _todos_temp_ : [];

let todos = reactive(_todos_temp_);

watch(
  todos,
  () => {
    localStorage.setItem("colored_todos", JSON.stringify(todos));
  },
  { deep: true }
);

function moveTodo(from, to) {
  var element = todos[from];
  todos.splice(from, 1);
  todos.splice(to, 0, element);
}
</script>

<style>
@import url("https://fonts.googleapis.com/css2?family=Anta&display=swap");

.anta-regular,
body {
  font-family: "Anta", sans-serif;
  font-weight: 400;
  font-style: normal;
}

.flex {
  display: flex;
}

.jc-center {
  justify-content: center;
}

.jc-between {
  justify-content: space-between;
}

.mb-1 {
  margin-bottom: 0.5rem;
}

.gap > *:not(:last-child) {
  margin-right: 5px;
}

.gap-v > *:not(:last-child) {
  margin-bottom: 5px;
}

.ai-center {
  align-items: center;
}

@media screen and (max-width: 1024px) {
  .auto-col {
    flex-direction: column;
    gap: 5px;
  }
}

.todo-container {
  width: 100%;
  display: flex;
  flex-direction: column;
}
</style>
