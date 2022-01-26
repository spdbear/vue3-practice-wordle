<script setup lang="ts">
import { ref, computed } from 'vue'

const props = defineProps<{
  index: number
  initialText: string
  canInput: boolean
}>()

const emit = defineEmits<{
  (name: 'change', updated: string): void
  (name: 'submit', updated: { text: string; index: number }): void
}>()

const texts = ref(props.initialText)

const hasNoTextError = computed(() => texts.value.length === 0)
const hasLongTextError = computed(() => texts.value.length > 10)

const handleChange = (e: Event) => {
  const { target } = e
  if (!(target instanceof HTMLInputElement)) return
  emit('change', target.value)
}

const handleSubmit = (e: Event) => {
  emit('submit', { text: texts.value, index: props.index })
}
</script>

<template>
  <div class="flex">
    <input
      :class="`rounded border-2 border-blue-300 bg-gray-100 p-2 font-mono uppercase text-gray-700 shadow-md focus:bg-white ${
        hasLongTextError && 'error'
      } disabled:border-gray-500 disabled:bg-gray-200`"
      :disabled="!canInput"
      v-model="texts"
      maxlength="5"
      placeholder="此処入力"
      @change="handleChange"
    />
    <button
      class="ml-1 rounded bg-blue-400 px-3 shadow-sm shadow-slate-600"
      :disabled="!canInput"
      @click="handleSubmit"
    >
      決
    </button>
  </div>
</template>

<style scoped>
.error {
  @apply border-red-500 bg-red-100 focus:bg-red-100;
}
</style>
