<script setup lang="ts">
import { ref, computed } from 'vue'
const props = defineProps<{
  index: number
  text: string
  time: number
  initialChecked: boolean
}>()
const emit = defineEmits<{ (name: 'click', event: Event): void }>()

const checked = ref(props.initialChecked)

const id = computed(() => props.index.toString())

const handleClick = (e: Event) => {
  emit('click', e)
}
</script>

<template>
  <div
    class="flex items-center mt-2 mb-2 p-2 border-solid border-2 border-blue-500 rounded"
  >
    <input :id="id" type="checkbox" v-model="checked" />
    <label :for="id" class="flex">
      <div class="block ml-1">
        {{ text }}
      </div>
      <div class="block ml-1">
        {{ time }}
      </div>
    </label>
  </div>
</template>

<style scoped></style>
