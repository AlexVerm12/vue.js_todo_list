<template>
  <div class="bg-gray-300 text-white w-1/2 m-auto mt-12">
    <div class="text-center border-b-2 border-black-300 py-4">
      <h1 class="text-3xl py-4">Unsere Todos</h1>
      <p class="text-xl">Offene Todos: {{ todos.length }}</p>
    </div>
    <div v-for="(todo, index) in todos" :key="todo.todo">
      <TodoList :todoprop="todo" :todoindex="index" @toggledone-index="toggleDone" />
    </div>
  </div>
</template>

<script>
import TodoList from "./components/TodoList.vue";

export default {
  name: "App",
  data() {
    return {
      todos: [
        { todo: "Einkaufen", done: false },
        { todo: "Sport", done: false },
        { todo: "Programmieren", done: true },
      ],
    };
  },
  methods:{
    toggleDone(index){
      this.todos[index].done = !this.todos[index].done;
    }
  },
  components: {
    TodoList,
  },
};
</script>

<style>
</style>
