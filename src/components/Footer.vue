<script setup lang="ts">
import { PropType } from "vue";

export interface Stats {
  active: number;
  done: number;
}

const props = defineProps({
  stats: {
    type: Object as PropType<Stats>,
    required: true,
  },
});
</script>

<template>
  <footer class="container h-15 mt-6 flex flex-col items-center justify-center">
    <p class="text-gray-200">
      {{ props.stats.active }} more to do, {{ props.stats.done }} done
    </p>
  </footer>
</template>
