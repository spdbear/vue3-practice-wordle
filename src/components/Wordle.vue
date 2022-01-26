<script setup lang="ts">
import { ref, computed } from 'vue'
import WordInput from './WordInput.vue'
import WordStatus from './WordStatus.vue'
import CharList from './CharList.vue'

import {
  title,
  answerList,
  availableWordList,
  CHALLENGE_TIMES,
} from '../assets/sample'

const answer = answerList[Math.floor(Math.random() * answerList.length)]
const charStr = Array.from(new Set(availableWordList.join('').split('')))
  .sort()
  .join('')

const wordList = ref<string[]>(
  [...Array(CHALLENGE_TIMES)].fill([...Array(answer.length).fill('_')].join(''))
)

const currentNum = ref(0)
const canInputList = computed(() =>
  [...Array(CHALLENGE_TIMES)].map((e, i) => i === currentNum.value)
)

const handleSubmit = (obj: { text: string; index: number }) => {
  if (availableWordList && !availableWordList.includes(obj.text)) return
  wordList.value[currentNum.value] = obj.text
  currentNum.value++
}
</script>

<template>
  <div class="mx-auto flex flex-col">
    <header class="m-4 mx-auto text-xl font-bold">{{ title }}</header>
    <div class="flex flex-col justify-center">
      <template v-for="i in CHALLENGE_TIMES">
        <div class="flex items-center justify-center">
          <WordInput
            class="m-1"
            :index="i"
            :initial-text="''"
            :can-input="canInputList[i - 1]"
            @submit="handleSubmit"
          />
          <WordStatus
            class="m-1"
            :index="i"
            :word="wordList[i - 1]"
            :answer="answer"
          />
        </div>
      </template>
      <CharList
        class="mt-4"
        :char-str="charStr"
        :word-list="wordList"
        :answer="answer"
      />
    </div>
  </div>
</template>

<style scoped></style>
