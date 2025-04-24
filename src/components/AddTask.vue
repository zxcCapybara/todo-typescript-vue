<script setup lang="ts">
import { ref } from "vue";
import { Todo } from "@/types/Todo";

const isModal = ref<boolean>(false);
const todoText = ref<string>("");

const closeModal = () => {
  isModal.value = false;
  todoText.value = "";
};

const emit = defineEmits<{
  (e: "addTodo", todo: Todo): void;
}>();

const addTodo = () => {
  if (todoText.value.trim()) {
    emit("addTodo", {
      id: Date.now(),
      text: todoText.value,
      completed: false,
    });
    todoText.value = "";
  }
};
</script>

<template>
  <form
    @submit.prevent="addTodo"
    v-if="isModal"
    class="container flex relative h-[10rem] mt-10 flex-col justify-end"
  >
    <button type="button" @click="closeModal" class="absolute top-1 right-3 text-xl">
      x
    </button>
    <input
      @keyup.enter="addTodo"
      v-model="todoText"
      type="text"
      class="m-5 h-[2rem] rounded-xl px-5 border-1 border-red-600 outline-none"
      placeholder="Add task..."
    />
    <button
      type="submit"
      class="m-5 h-[2rem] rounded-xl mt-1 bg-red-600 text-white hover:bg-red-500"
    >
      Add task
    </button>
  </form>
  <button type="button"
    v-else
    @click="isModal = true"
    class="container h-[4rem] mt-10 flex items-center justify-center gap-5 text-[2rem] text-red-500"
  >
    +
  </button>
</template>
