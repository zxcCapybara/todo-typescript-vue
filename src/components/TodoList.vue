<script setup lang="ts">
import { Todo } from "@/types/Todo";
import TodoItem from "./TodoItem.vue";
import { PropType } from "vue";

const props = defineProps({
  todos: {
    type: Array as PropType<Todo[]>,
    required: true,
  },
});

const emit = defineEmits<{
  (e: "toggleTodo", id: number): void;
  (e: "removeTodo", id: number): void;
}>();

const toggleTodo = (id: number) => {
  emit("toggleTodo", id);
};

const removeTodo = (id: number) => {
  emit("removeTodo", id);
};
</script>

<template>
  <ul class="flex flex-col gap-5 mt-15 w-full">
    <TodoItem
      v-if="props.todos.length"
      v-for="todo in props.todos"
      :key="todo.id"
      :todo="todo"
      @toggle-todo="toggleTodo"
      @remove-todo="removeTodo"
    />
    <p v-else class="text-center text-gray-300">empty list</p>
  </ul>
</template>
