<template>
  <div class="min-h-screen bg-gray-100 text-gray-800 font-sans p-4">
    <h1 class="text-3xl font-bold mb-6 text-center">🎨 PalettePulse</h1>
    <PaletteGenerator @palette-saved="updatePalettes" />
    <SavedPalettes :palettes="palettes" class="mt-10" />
  </div>
</template>

<script setup>
import { ref, onMounted } from 'vue'
import PaletteGenerator from './components/PaletteGenerator.vue'
import SavedPalettes from './components/SavedPalettes.vue'

const palettes = ref([])

const updatePalettes = () => {
  // Load palettes from localStorage, newest first
  palettes.value = JSON.parse(localStorage.getItem('palettes') || '[]').reverse()
}

onMounted(updatePalettes)
</script>
