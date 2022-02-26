<template>
  <form
    class="flex justify-between space-x-2 md:space-x-4 w-full"
    @submit.prevent="addTodo"
  >
    <input
      v-model="todo.name"
      type="text"
      placeholder="Enter Todo Name"
      class="border-gray-300 rounded-md grow focus:ring-primary focus:ring-2 focus:border-none"
    >
    <button type="submit" class="bg-primary p-2 md:p-4 text-white rounded-md">
      Add Todo
    </button>
  </form>
</template>
<script setup lang="ts">
import { reactive } from 'vue'
import type { Todo } from '@/types/todo'

const emit = defineEmits<{ (e: 'todoAdded', todo: Todo): void }>()

const todo = reactive({
  id: Date.now(),
  name: '',
  completed: false,
  time: new Date(),
})

function addTodo() {
  if (!todo.name) return

  const newTodo = {
    id: Date.now(),
    name: todo.name,
    completed: false,
    time: new Date().toDateString(),
  }

  emit('todoAdded', newTodo)

  todo.name = ''
}
</script>
