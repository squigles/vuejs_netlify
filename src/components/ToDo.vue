<template>
  <input 
  type="text"
  placeholder="Enter todo and hit enter"
  class="border-orange-300 border-2 w-full p-2 rounded"
  v-model="todoTitle"
  @keyup.enter="addToDo"
  >
  <div class="mt-4">
    <div v-for="(todo, index) in todos" :key="index" class="flex border-gray-300 border-b-2 mb-2 p-1">
      <div class="w-5/6 text-lg" :class="{'line-through text-green-600':todo.complete}">{{todo.title}}</div>
      <div class="w-1/6 flex">
        <div class="mr-4">
          <button 
          class="bg-red-500 text-white text-xs font-bold px-2 rounded cursor-pointer hover: bg-red-600"
          @click="deleteTodo(index)"
          >X</button>
        </div>
        <div>
          <input 
          type="checkbox" 
          :checked="todo.complete"
          @click="toggleTodo(index)"
          >
        </div>

      </div>
    </div>
  </div>
</template>

<script>
import { ref } from "vue"
export default {
  setup() {
    var todoTitle = ref("")
    const todos = ref([])
    function addToDo() {
      todos.value.push({ title: todoTitle.value, complete: false})
      todoTitle.value = ""
    }
    function toggleTodo(index) {
      todos.value[index].complete = !todos.value[index].complete
    }
    function deleteTodo(index) {
      todos.value.splice(index, 1)
    }
    return { todoTitle, todos, addToDo, toggleTodo, deleteTodo}
  }
}
</script>


<style></style>