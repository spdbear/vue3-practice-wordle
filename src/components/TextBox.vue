<script setup lang="ts">
import { ref, computed } from 'vue'

const props = defineProps<{
  initialText: string
}>()

const emit = defineEmits<{ (name: 'change', updatedText: string): void }>()

const texts = ref(props.initialText)

const handleChange = (e: Event) => {
  const { target } = e
  if (!(target instanceof HTMLInputElement)) return
  emit('change', target.value)
}
</script>

<template>
  <div>
    <input
      class="bg-gray-100 focus:bg-white p-2 border-2 border-gray-500 shadow-md rounded text-gray-700"
      v-model="texts"
      placeholder="input here"
      @change="handleChange"
    />
  </div>
</template>

<style scoped></style>
