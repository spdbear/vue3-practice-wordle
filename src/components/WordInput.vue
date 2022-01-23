<script setup lang="ts">
import { ref, computed } from 'vue'

const props = defineProps<{
  index: number
  initialText: string
}>()

const emit =
  defineEmits<{
    (name: 'change', updatedText: string): void
    (name: 'enter', updatedText: string): void
  }>()

const texts = ref(props.initialText)

const hasNoTextError = computed(() => texts.value.length === 0)
const hasLongTextError = computed(() => texts.value.length > 10)

const handleChange = (e: Event) => {
  const { target } = e
  if (!(target instanceof HTMLInputElement)) return
  emit('change', target.value)
}
</script>

<template>
  <div>
    <input
      :class="`bg-gray-100 focus:bg-white p-2 border-2 border-gray-500 shadow-md rounded text-gray-700 ${
        (hasLongTextError) && 'error'
      }`"
      v-model="texts"
      maxlength="5"
            placeholder="input here"
      @change="handleChange"
    />
  </div>
</template>

<style scoped>
.error {
  @apply border-red-500 bg-red-100 focus:bg-red-100;
}
</style>
