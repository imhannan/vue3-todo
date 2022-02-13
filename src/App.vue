<script setup>
import TodoList from "./components/TodoList.vue";
</script>

<template>
  <header class="p-4 md:p-8">
    <h1 class="text-center text-xl md:text-2xl text-white font-bold">
      Vue 3 Todo App
    </h1>
  </header>

  <main
    class="main bg-white rounded-lg drop-shadow-lg p-4 md:p-8 flex flex-col space-y-2 md:space-y-4"
  >
    <TodoList />
  </main>
</template>

<style></style>
