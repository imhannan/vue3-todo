<template>
  <div class="flex items-center space-x-2 md:space-x-4">
    <input
      :checked="todo.completed"
      type="checkbox"
      class="w-4 h-4 md:w-8 md:h-8 rounded-full text-primary border-gray-300 focus:ring-primary"
      @click="toggleTodo"
    >
    <div class="flex flex-col space-y-1 md:space-y-2">
      <h2 class="font-bold text-lg md:text-xl">
        {{ todo.name }}
      </h2>
      <span class="text-gray-500">{{
        dayjs(todo.time, 'MM-DD-YYYY').fromNow()
      }}</span>
    </div>
  </div>
</template>
<script setup lang="ts">
import dayjs from 'dayjs'
import relativeTime from 'dayjs/plugin/relativeTime'
import type { Todo } from '@/types/todo'
dayjs.extend(relativeTime)

interface Props {
  todo: Todo
}

const props = defineProps<Props>()

const emit = defineEmits<{
  (e: 'todoToggled', todo: Todo): void
}>()

function toggleTodo() {
  emit('todoToggled', {
    id: props.todo.id,
    completed: !props.todo.completed,
    name: props.todo.name,
    time: props.todo.time,
  })
}
</script>
