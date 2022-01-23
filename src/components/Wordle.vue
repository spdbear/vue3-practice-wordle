<script setup lang="ts">
import { ref, onMounted, reactive, readonly } from 'vue'
import WordInput from './WordInput.vue'

defineProps<{ msg: string }>()

const answer = 'earth'
const wordList = ['apple', 'empty', 'house', 'right', 'toast']
</script>

<template>
  <header>Wordle</header>
  <div class="flex flex-col">
    <template v-for="i in 6">
      <WordInput :index="i" :initial-text="''" />
    </template>
  </div>
</template>

<style scoped></style>
