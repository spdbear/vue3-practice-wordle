<script setup lang="ts">
import { ref, computed } from 'vue'

const props = defineProps<{
  index: number
  word: string
  answer: string
}>()

const wordArray = computed(() => props.word.split(''))
const answerArray = computed(() => props.answer.split(''))

const getColor = (char: string, index: number) => {
  let isGreen = false
  let isYellow = false
  answerArray.value.forEach((ansChar: string, ansIndex: number) => {
    if (char === ansChar) {
      if (index === ansIndex) {
        isGreen = true
      } else {
        isYellow = true
      }
    }
  })
  if (isGreen) return 'green'
  if (isYellow) return 'yellow'
  return 'gray'
}
</script>

<template>
  <template v-for="(char, i) in wordArray">
    <template v-if="getColor(char, i) === 'green'">
      <div class="m-1 bg-green-300 px-3 py-2 align-middle font-mono uppercase">
        {{ char }}
      </div>
    </template>
    <template v-else-if="getColor(char, i) === 'yellow'">
      <div class="m-1 bg-yellow-300 px-3 py-2 align-middle font-mono uppercase">
        {{ char }}
      </div>
    </template>
    <template v-else>
      <div class="m-1 bg-gray-300 px-3 py-2 align-middle font-mono uppercase">
        {{ char }}
      </div>
    </template>
  </template>
</template>

<style scoped>
.error {
  @apply border-red-500 bg-red-100 focus:bg-red-100;
}
</style>
