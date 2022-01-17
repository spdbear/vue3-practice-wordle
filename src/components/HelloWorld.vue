<script setup lang="ts">
import { ref, onMounted, reactive, readonly } from 'vue'
import Button from './Button.vue'

defineProps<{ msg: string }>()

const count = ref(0)

const obj = reactive({ count })

const objCopied = readonly(obj)

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
    <Button :text="`count is: ${count}`" @click="obj.count++" />
  </div>
</template>

<style scoped></style>
