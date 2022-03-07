<script setup lang="ts">
import { ref } from 'vue';

interface TodoItem {
  text: string;
  done: boolean;
}
const newTodo = ref('');
const todos = ref<TodoItem[]>([]);

const addTodo = () => {
  todos.value.push({
    text: newTodo.value,
    done: false,
  });
  newTodo.value = '';
};
</script>

<template>
  <h1>Todo List</h1>
  <label>
    Add Todo:
    <input type="text" v-model="newTodo" @keyup.enter="addTodo" />
  </label>

  <ul>
    <li
      v-for="(todo, index) in todos"
      :key="index"
      :class="{ done: todo.done }"
    >
      <input type="checkbox" v-model="todo.done" />
      <span :data-done="todo.done">{{ todo.text }}</span>
    </li>
  </ul>
</template>

<style scoped>
input[type='text'] {
  width: 100%;
}
ul {
  list-style: none;
  padding: 0;
  text-align: left;
}
span[data-done='true'] {
  text-decoration: line-through;
}
</style>
