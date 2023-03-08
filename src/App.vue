<template>
  <div class="rounded bg-gray-300 text-white w-1/2 m-auto mt-12">
    <div class="text-center border-b-2 border-black-300 py-4">
      <h1 class="text-3xl py-4">Unsere Todos</h1>
      <p class="text-xl" v-if="openTodos.length > 0">Offene Todos: {{ openTodos.length }}</p>
      <p class="text-xl" v-else>
         Keine Todos. Gratuliere!
      </p>
      <div class="mt-4">
        <input
          type="text"
          class="py-2 px-2 rounded text-black"
          v-model="newTodo"
        />
        <button class="bg-blue-400 py-2 px-2 mx-2 rounded" @click="addTodo">
          Add todo
        </button>
      </div>
    </div>
    <div v-for="(todo, index) in todos" :key="todo.todo">
      <TodoList
        :todoprop="todo"
        :todoindex="index"
        @toggledone-index="toggleDone"
        @removetodo-index="removeTodo"
      />
    </div>
  </div>
</template>

<script>
import TodoList from "./components/TodoList.vue";

export default {
  name: "App",
  data() {
    return {
      newTodo: "",
      todos: [
        { todo: "Einkaufen", done: false },
        { todo: "Sport", done: false },
        { todo: "Programmieren", done: false },
      ],
    };
  },
  methods: {
    toggleDone(index) {
      this.todos[index].done = !this.todos[index].done;
      this.storeTodos();
    },

    removeTodo(index) {
      this.todos.splice(index, 1);
      this.storeTodos();
    },

    addTodo() {
      if (this.newTodo.trim() === "") {
        return;
      }
      this.todos.push({ todo: this.newTodo, done: false });
      this.storeTodos();
      this.newTodo= "";
    },

    storeTodos(){
      localStorage.setItem("todos", JSON.stringify(this.todos))
    }
  },
  mounted(){
    let data = localStorage.getItem("todos");
    if(data !== "" && data !== null){
    this.todos = JSON.parse(data);
    } else {
      this.todos = [];
    }
  },
  computed: {
    openTodos() {
      const openTodos = this.todos.filter((todo)=> {
        return !todo.done;
      });
      return openTodos;
    },
  },

  components: {
    TodoList,
  },
};
</script>

<style>
</style>
