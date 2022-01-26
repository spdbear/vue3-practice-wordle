<script setup lang="ts">
import { ref, computed } from 'vue'

const props = defineProps<{
  initialText: string
}>()

const emit = defineEmits<{ (name: 'change', updatedText: string): void }>()

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
      :class="`rounded border-2 border-gray-500 bg-gray-100 p-2 text-gray-700 shadow-md focus:bg-white ${
        (hasNoTextError || hasLongTextError) && 'error'
      }`"
      v-model="texts"
      placeholder="input here"
      @change="handleChange"
    />
    <div class="text-red-400" v-if="hasNoTextError">Please input text.</div>
    <div class="text-red-400" v-if="hasLongTextError">
      Text is limited to 10 characters.
    </div>
  </div>
</template>

<style scoped>
.error {
  @apply border-red-500 bg-red-100 focus:bg-red-100;
}
</style>
