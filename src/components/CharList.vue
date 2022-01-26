<script setup lang="ts">
import { ref, computed } from 'vue'

const props = defineProps<{
  charStr: string
  wordList: string[]
  answer: string
}>()

const charArray = computed(() => props.charStr.split(''))
const wordArray = computed(() => props.wordList.join('').split(''))

const getColor = (char: string) => {
  let isUsed = false
  wordArray.value.forEach((usedChar: string) => {
    if (char === usedChar) {
      isUsed = true
    }
  })
  if (isUsed) return 'gray'
  return 'white'
}
</script>

<template>
  <div class="mx-auto grid max-w-xl grid-cols-10">
    <template v-for="(char, i) in charArray">
      <template v-if="getColor(char) === 'gray'">
        <div class="m-1 bg-gray-300 px-3 py-2 align-middle font-mono uppercase">
          {{ char }}
        </div>
      </template>
      <template v-else>
        <div class="m-1 bg-white px-3 py-2 align-middle font-mono uppercase">
          {{ char }}
        </div>
      </template>
    </template>
  </div>
</template>

<style scoped>
.error {
  @apply border-red-500 bg-red-100 focus:bg-red-100;
}
</style>
