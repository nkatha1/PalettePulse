<template>
  <div>
    <h2 class="text-2xl font-semibold mb-4">❤️ Saved Palettes</h2>

    <div v-if="palettes.length === 0" class="text-gray-500">
      No palettes saved yet.
    </div>

    <div v-else class="space-y-6">
      <div
        v-for="(palette, index) in palettes"
        :key="palette.timestamp"
        class="bg-white p-4 rounded-lg shadow"
      >
        <div class="mb-2 font-medium text-gray-700">
          "{{ palette.prompt || 'No description' }}"
        </div>
        <div class="grid grid-cols-5 gap-2">
          <div
            v-for="(color, idx) in palette.colors"
            :key="idx"
            :style="{ backgroundColor: color }"
            class="h-16 rounded"
            :title="color"
          ></div>
        </div>
      </div>
    </div>
  </div>
</template>

<script setup>
defineProps({
  palettes: {
    type: Array,
    default: () => []
  }
})
</script>