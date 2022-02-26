<template>
  <section class="flex justify-between space-x-2">
    <button
      class="group flex justify-center grow items-center space-x-2 p-1 md:p-2 rounded-md"
      :class="{ 'bg-primary': activeTab === 'all' }"
      @click="filter('all')"
    >
      <span :class="{ 'text-white': activeTab === 'all' }">All</span><span
        class="bg-blue-200 text-black inline-block p-1 text-xs rounded-full"
      >{{ todosCount }}</span>
    </button>
    <button
      class="group flex justify-center grow items-center space-x-2 p-1 md:p-2 rounded-md"
      :class="{ 'bg-primary': activeTab === 'pending' }"
      @click="filter('pending')"
    >
      <span :class="{ 'text-white': activeTab === 'pending' }">Pending</span><span
        class="bg-yellow-300 text-white inline-block p-1 text-xs rounded-full"
      >{{ pendingCount }}</span>
    </button>
    <button
      class="group flex justify-center grow items-center space-x-2 p-1 md:p-2 rounded-md"
      :class="{ 'bg-primary': activeTab === 'completed' }"
      @click="filter('completed')"
    >
      <span :class="{ 'text-white': activeTab === 'completed' }">Completed</span><span
        class="bg-green-500 text-white inline-block p-1 text-xs rounded-full"
      >{{ completedCount }}</span>
    </button>
  </section>
</template>
<script setup lang="ts">
import { computed } from 'vue'
import type { Todo } from '@/types/todo'
const props = defineProps<Props>()

interface Props {
  todos: Todo[]
  activeTab: string
}
const emit = defineEmits<{ (e: 'filtered', type: string): void }>()

const todosCount = computed<number>(() => {
  return props.todos.length
})

const pendingCount = computed<number>(() => {
  return props.todos.filter(todo => !todo.completed).length
})

const completedCount = computed<number>(() => {
  return props.todos.filter(todo => todo.completed).length
})

function filter(type: string) {
  emit('filtered', type)
}
</script>
