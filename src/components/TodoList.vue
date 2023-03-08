<template>
  <div
    class="flex justify-between py-2 px-2"
    :class="{ 'bg-green-600': this.todo.done }"
  >
    <p @click="toggleTodo" class="text-xl cursor-pointer">{{ todo.todo }}</p>
    <button class="bg-red-600 py-1 px-2 rounded" @click="removeTodo">
      Delete
    </button>
  </div>
</template>
<script>
export default {
  name: "TodoList",
  props: ["todoprop", "todoindex"],
  data() {
    return {
      todo: this.todoprop,
    };
  },
  methods: {
    toggleTodo() {
      this.$emit("toggledone-index", this.todoindex);
    },
    removeTodo() {
      this.$emit("removetodo-index", this.todoindex);
    },
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style>
</style>
