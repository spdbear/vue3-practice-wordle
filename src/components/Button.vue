<script setup lang="ts">
import { ref, onMounted, reactive, readonly } from 'vue'
const props = defineProps<{ text: string }>()
const emit = defineEmits<{ (name: 'click', event: Event): void }>()

const handleClick = (e: Event) => {
  emit('click', e)
}
</script>

<template>
  <button
    class="bg-blue-500 hover:bg-blue-700 text-white font-bold py-2 px-4 rounded"
    type="button"
    @click="handleClick"
  >
    {{ text }}
  </button>
</template>

<style scoped></style>
