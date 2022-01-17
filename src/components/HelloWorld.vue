<script setup lang="ts">
import { ref, onMounted, reactive, readonly } from 'vue'
import Button from './Button.vue'
import Todo from './Todo.vue'
import Todo1 from './Todo.vue'

defineProps<{ msg: string }>()

const count = ref(0)

const obj = reactive({ count })

const objCopied = readonly(obj)

const todoList = [
  {
    text: 'やる',
    time: 100,
    checked: false,
  },
  {
    text: 'やる2',
    time: 200,
    checked: false,
  },
]

onMounted(() => {
  setInterval(() => count.value--, 1000)
})
</script>

<template>
  <div class="m-4">
    <h1 class="mb-4 text-3xl font-bold underline">{{ msg }}</h1>
    <Button :text="'Click'" @click="count++" />
    <div class="m-4">
      {{ obj.count }}
    </div>
    <template v-for="(todo, index) in todoList">
      <Todo
        :index="index"
        :text="todo.text"
        :time="todo.time"
        :initial-checked="todo.checked"
      ></Todo>
    </template>
    <Button :text="`count is: ${count}`" @click="obj.count++" />
  </div>
</template>

<style scoped></style>
