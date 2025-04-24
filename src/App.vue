<script setup lang="ts">
import Header from "./components/Header.vue";
import Filters from "./components/Filters.vue";
import TodoList from "./components/TodoList.vue";
import AddTask from "./components/AddTask.vue";
import Footer, { Stats } from "./components/Footer.vue";
import { Todo } from "./types/Todo";
import { computed, ref } from "vue";
import { activeFilters } from "./types/activeFilters";

interface State {
  todos: Todo[];
  activeFilter: activeFilters;
}

const todos = ref<State>({
  todos: [],
  activeFilter: "All",
});
const appTodo = (todo: Todo) => {
  todos.value.todos.push(todo);
};
const toggleTodo = (id: number) => {
  const targetTodo = todos.value.todos.find((todo: Todo) => todo.id === id);
  if (targetTodo) {
    targetTodo.completed = !targetTodo.completed;
  }
};

const removeTodo = (id: number) => {
  todos.value.todos = todos.value.todos.filter((todo: Todo) => todo.id !== id);
};

const setFilter = (filter: activeFilters) => {
  todos.value.activeFilter = filter;
};

const filtredTodos = computed<Todo[]>(() => {
  switch (todos.value.activeFilter) {
    case "Active":
      return activeTodos.value;
    case "Done":
      return completedTodo.value;

    case "All":
    default:
      return todos.value.todos;
  }
});

const stats = computed<Stats>(() => {
  return {
    active: activeTodos.value.length,
    done: completedTodo.value.length,
  };
});

const activeTodos = computed<Todo[]>(() => {
  return todos.value.todos.filter((todo) => !todo.completed);
});

const completedTodo = computed<Todo[]>(() => {
  return todos.value.todos.filter((todo) => todo.completed);
});
</script>

<template>
  <main
    class="flex justify-center items-center flex-col h-screen mx-7 sm:w-[30rem] sm:m-auto"
  >
    <Header />
    <Filters :active-filter="todos.activeFilter" @set-filter="setFilter" />
    <TodoList
      :todos="filtredTodos"
      @toggle-todo="toggleTodo"
      @remove-todo="removeTodo"
    />
    <AddTask @add-todo="appTodo" />
    <Footer :stats="stats" />
  </main>
</template>

<style scoped>
main {
  touch-action: manipulation;
}
</style>
