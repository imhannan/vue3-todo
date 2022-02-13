<template>
  <form
    @submit.prevent="addTodo"
    class="flex justify-between space-x-2 md:space-x-4 w-full"
  >
    <input
      v-model="todo.name"
      type="text"
      placeholder="Enter Todo Name"
      class="border-gray-300 rounded-md grow focus:ring-primary focus:ring-2 focus:border-none"
    />
    <button type="submit" class="bg-primary p-2 md:p-4 text-white rounded-md">
      Add Todo
    </button>
  </form>
</template>
<script setup>
import { reactive } from "vue";

const emit = defineEmits(["todoAdded"]);

const todo = reactive({
  id: Date.now(),
  name: "",
  completed: false,
  time: new Date(),
});

function addTodo() {
  if (!todo.name) {
    alert("Please enter a todo name");
    return;
  }

  const newTodo = {
    id: Date.now(),
    name: todo.name,
    completed: false,
    time: new Date(),
  };

  emit("todoAdded", newTodo);

  todo.name = "";
}
</script>
