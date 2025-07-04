<template>
  <div class="max-w-xl mx-auto bg-white rounded-lg shadow p-6">
    <input
      v-model="prompt"
      type="text"
      placeholder="Describe a mood or theme..."
      class="w-full p-3 border rounded mb-4"
    />
    <button @click="generatePalette" class="bg-blue-600 text-white px-4 py-2 rounded">
      Generate Palette
    </button>

    <div v-if="palette.length" class="mt-6 grid grid-cols-5 gap-2">
      <div
        v-for="(color, index) in palette"
        :key="index"
        :style="{ backgroundColor: color }"
        class="h-24 rounded relative"
      >
        <span class="absolute bottom-1 left-1 text-xs text-white bg-black bg-opacity-50 px-1 rounded">
          {{ color }}
        </span>
      </div>
    </div>

    <button
      v-if="palette.length"
      @click="savePalette"
      class="mt-4 text-sm text-blue-600 hover:underline"
    >
      ❤️ Save this palette
    </button>
  </div>
</template>

<script setup>
import { ref } from 'vue'

const prompt = ref('')
const palette = ref([])

const emit = defineEmits(['palette-saved'])

const generatePalette = () => {
  const colors = Array.from({ length: 5 }, () => randomColor())
  palette.value = colors
}

const savePalette = () => {
  const saved = JSON.parse(localStorage.getItem('palettes') || '[]')
  saved.push({ colors: palette.value, prompt: prompt.value, timestamp: Date.now() })
  localStorage.setItem('palettes', JSON.stringify(saved))

  emit('palette-saved')  // Notify parent to update saved palettes
}

const randomColor = () => {
  return '#' + Math.floor(Math.random() * 16777215).toString(16).padStart(6, '0')
}
</script>