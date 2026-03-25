<script setup>
import { computed } from "vue";

const props = defineProps({
  type: {
    type: String,
    required: true,
  },
  message: {
    type: String,
    required: true,
  },
});

const isError = computed(() => props.type === "error");
</script>

<template>
  <div
    :class="isError ? 'bg-red-600' : 'bg-green-600'"
    class="text-white text-center p-3 uppercase font-bold mb-3 rounded-md"
    role="alert"
  >
    {{ message }}
  </div>
</template>
