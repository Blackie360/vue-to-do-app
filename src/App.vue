<template>
  <div class="flex flex-col items-center justify-center h-screen bg-gray-900">
    <div class="w-full max-w-lg bg-gray-800 rounded-lg shadow-lg">
      <div class="px-6 py-4">
        <h1 class="text-3xl font-bold text-gray-300 mb-4">To-Do List</h1>
        <div class="mb-4">
          <input type="text" v-model="newTodo" placeholder="Add new task" class="bg-gray-700 rounded-lg py-2 px-4 text-gray-300 w-full">
        </div>
        <button class="bg-indigo-500 hover:bg-indigo-600 text-white font-bold py-2 px-4 rounded-lg mb-4" @click="addTodo">Add Task</button>
        <ul>
          <li v-for="(todo, index) in todos" :key="index" class="flex justify-between items-center bg-gray-700 py-2 px-4 rounded-lg mb-2">
            <div class="flex-grow pr-4">
              <input type="text" v-model="todo.title" class="bg-transparent text-gray-300 w-full" :class="{ 'line-through': todo.completed }" @keydown.enter="editTodo" @blur="editTodo">
            </div>
            <div>
              <button class="bg-gray-600 hover:bg-gray-700 text-white font-bold py-2 px-4 rounded-lg mr-2" @click="toggleCompletion(todo)">{{ todo.completed ? 'Uncheck' : 'Check' }}</button>
              <button class="bg-red-600 hover:bg-red-700 text-white font-bold py-2 px-4 rounded-lg" @click="deleteTodo(index)">Delete</button>
            </div>
          </li>
        </ul>
      </div>
    </div>
  </div>
</template>

<script>
  export default {
    data() {
      return {
        newTodo: '',
        todos: [
          { title: 'Finish homework', completed: false },
          { title: 'Buy groceries', completed: true },
          { title: 'Clean the house', completed: false }
        ]
      }
    },
    methods: {
      addTodo() {
        if (this.newTodo.trim()) {
          this.todos.push({
            title: this.newTodo,
            completed: false
          })
          this.newTodo = ''
        }
      },
      editTodo() {
        // do nothing, just allow editing to complete
      },
      toggleCompletion(todo) {
        todo.completed = !todo.completed
      },
      deleteTodo(index) {
        this.todos.splice(index, 1)
      }
    }
  }
</script>

<style>
  /* Styles for text decoration on completed tasks */
  .line-through {
    text-decoration: line-through;
  }
</style>
