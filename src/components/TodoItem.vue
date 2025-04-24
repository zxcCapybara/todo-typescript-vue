<script setup lang="ts">
import { Todo } from "@/types/Todo";
import type { PropType } from "vue";

const props = defineProps({
  todo: {
    type: Object as PropType<Todo>,
    required: true,
  },
});

const emit = defineEmits<{
  (e: "toggleTodo", id: number): void;
  (e: "removeTodo", id: number): void;
}>();

const toggleTodo = () => {
  emit("toggleTodo", props.todo.id);
};

const removeTodo = () => {
  emit("removeTodo", props.todo.id);
};
</script>

<template>
  <li
    class="container h-[3rem] flex items-center pl-5 relative"
    :class="{ 'todo-done': todo.completed }"
    @click="toggleTodo"
  >
    <svg
      class="fill-white done"
      xmlns="http://www.w3.org/2000/svg"
      x="0px"
      y="0px"
      width="30"
      height="30"
      viewBox="0 0 50 50"
    >
      <path
        d="M 42.875 8.625 C 42.84375 8.632813 42.8125 8.644531 42.78125 8.65625 C 42.519531 8.722656 42.292969 8.890625 42.15625 9.125 L 21.71875 40.8125 L 7.65625 28.125 C 7.410156 27.8125 7 27.675781 6.613281 27.777344 C 6.226563 27.878906 5.941406 28.203125 5.882813 28.597656 C 5.824219 28.992188 6.003906 29.382813 6.34375 29.59375 L 21.25 43.09375 C 21.46875 43.285156 21.761719 43.371094 22.050781 43.328125 C 22.339844 43.285156 22.59375 43.121094 22.75 42.875 L 43.84375 10.1875 C 44.074219 9.859375 44.085938 9.425781 43.875 9.085938 C 43.664063 8.746094 43.269531 8.566406 42.875 8.625 Z"
      ></path>
    </svg>

    <p class="w-[80%] m-auto">{{ todo.text }}</p>
    <svg
      @click.stop="removeTodo"
      class="fill-red-500 lg:fill-gray-200 delete lg:hidden absolute right-5"
      xmlns="http://www.w3.org/2000/svg"
      x="0px"
      y="0px"
      width="20"
      height="20"
      viewBox="0 0 24 24"
    >
      <path
        d="M 10 2 L 9 3 L 4 3 L 4 5 L 5 5 L 5 20 C 5 20.522222 5.1913289 21.05461 5.5683594 21.431641 C 5.9453899 21.808671 6.4777778 22 7 22 L 17 22 C 17.522222 22 18.05461 21.808671 18.431641 21.431641 C 18.808671 21.05461 19 20.522222 19 20 L 19 5 L 20 5 L 20 3 L 15 3 L 14 2 L 10 2 z M 7 5 L 17 5 L 17 20 L 7 20 L 7 5 z M 9 7 L 9 18 L 11 18 L 11 7 L 9 7 z M 13 7 L 13 18 L 15 18 L 15 7 L 13 7 z"
      ></path>
    </svg>
  </li>
</template>

<style scoped>
.container:hover {
  cursor: pointer;
}

.container:hover .delete {
  display: block;
}

.delete:hover {
  fill: red;
}

.container:hover .done {
  fill: red;
}


</style>
