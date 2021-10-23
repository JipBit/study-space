<template>
  <div class="bg-[#1B1C1F] text-white mt-12 p-4 rounded-t-md">
      <div class="flex items-center mb-12">
          <svg xmlns="http://www.w3.org/2000/svg" width="32" height="32" viewBox="0 0 24 24" style="fill: rgba(255, 255, 255, 1);transform: ;msFilter:;"><path d="M12 2C6.486 2 2 6.486 2 12s4.486 10 10 10 10-4.486 10-10S17.514 2 12 2zm5 11h-4v4h-2v-4H7v-2h4V7h2v4h4v2z"></path></svg>
    
          <input v-model="todo" @keydown.enter="addTodo" class="bg-transparent border-0 text-white ml-2 outline-none w-full" type="text" placeholder="Enter todo here...">
      </div>

      <div class="space-y-3">
          <div v-for="todo in todos" :key="todo.id" class="bg-[#2B2D31] rounded-md p-3 flex items-center justify-between">
              <h1 @click="e => e.target.classList.toggle('line-through')" class="cursor-pointer">{{ todo.text }}</h1>

              <button @click="deleteTodo(todo.id)">
                  <svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24" style="fill: rgba(255, 255, 255, 1);transform: ;msFilter:;"><path d="M6 7H5v13a2 2 0 0 0 2 2h10a2 2 0 0 0 2-2V7H6zm10.618-3L15 2H9L7.382 4H3v2h18V4z"></path></svg>
              </button>
          </div>
      </div>
  </div>
</template>

<script>
const todoStorage = "TODO_STORAGE";

export default {
  data() {
    return {
      todo: "",
      todos: [],
    };
  },

  mounted() {
    if (localStorage.getItem(todoStorage))
      this.todos = JSON.parse(localStorage.getItem(todoStorage));
  },

  methods: {
    deleteTodo(todoId) {
      this.todos = this.todos.filter((todo) => todo.id !== todoId);
      localStorage.setItem(todoStorage, JSON.stringify(this.todos));
    },

    addTodo(todoId) {
      if (this.todo.length === 0) {
        return;
      } else {
        this.todos.push({
          id: Math.random(),
          text: this.todo,
        });

        this.todo = "";

        localStorage.setItem(todoStorage, JSON.stringify(this.todos));
      }
    },
  },
};
</script>

<style>
</style>