<script setup lang="ts">
import { activeFilters } from "@/types/activeFilters";
import { PropType } from "vue";
import { ref } from "vue";

interface State {
  filters: activeFilters[];
}

const props = defineProps({
  activeFilter: {
    type: String as PropType<activeFilters>,
    required: true,
  },
});

const filters = ref<State>({ filters: ["All", "Active", "Done"] });

const emit = defineEmits<{
  (e: "setFilter", filter: activeFilters): void;
}>();

const setFilter = (filter: activeFilters) => {
  emit('setFilter', filter)
};
</script>

<template>
  <ul class="flex justify-center gap-5 sm:gap-0 sm:justify-between w-full">
    <li v-for="filter in filters.filters" :key="filter">
      <button
        @click="setFilter(filter)"
        class="not-active w-[6rem] sm:w-[9rem] h-10"
        :class="{ 'active-btn': props.activeFilter === filter }"
      >
        {{ filter }}
      </button>
    </li>
  </ul>
</template>

<style scoped>
.active-btn {
  border-color: red !important;
  color: red !important;
}
</style>
