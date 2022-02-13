<template>
  <section class="flex justify-between space-x-2">
    <button
      @click="filter('all')"
      class="group flex justify-center grow items-center space-x-2 p-1 md:p-2 rounded-md"
      :class="{ 'bg-primary': activeTab === 'all' }"
    >
      <span :class="{ 'text-white': activeTab === 'all' }">All</span
      ><span
        class="bg-blue-200 text-black inline-block p-1 text-xs rounded-full"
        >{{ todosCount }}</span
      >
    </button>
    <button
      @click="filter('pending')"
      class="group flex justify-center grow items-center space-x-2 p-1 md:p-2 rounded-md"
      :class="{ 'bg-primary': activeTab === 'pending' }"
    >
      <span :class="{ 'text-white': activeTab === 'pending' }">Pending</span
      ><span
        class="bg-yellow-300 text-white inline-block p-1 text-xs rounded-full"
        >{{ pendingCount }}</span
      >
    </button>
    <button
      @click="filter('completed')"
      class="group flex justify-center grow items-center space-x-2 p-1 md:p-2 rounded-md"
      :class="{ 'bg-primary': activeTab === 'completed' }"
    >
      <span :class="{ 'text-white': activeTab === 'completed' }">Completed</span
      ><span
        class="bg-green-500 text-white inline-block p-1 text-xs rounded-full"
        >{{ completedCount }}</span
      >
    </button>
  </section>
</template>
<script setup>
import { computed } from "vue";
const props = defineProps({
  todos: {
    type: Array,
    required: true,
  },
  activeTab: {
    type: String,
    required: true,
  },
});
const emit = defineEmits(["filtered"]);

const todosCount = computed(() => {
  return props.todos.length;
});

const pendingCount = computed(() => {
  return props.todos.filter((todo) => !todo.completed).length;
});

const completedCount = computed(() => {
  return props.todos.filter((todo) => todo.completed).length;
});

function filter(type) {
  emit("filtered", type);
}
</script>
