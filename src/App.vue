<script setup>
import VTooltip from './components/VTooltip.vue'
</script>

<template>
  <div class="flex h-screen w-screen items-center justify-center bg-gray-900">
    <div
      class="flex min-h-[300px] min-w-[500px] items-center justify-center rounded bg-white p-5 text-center"
    >
      <v-tooltip>
        <template #activator="{ attrs }">
          <button v-bind="attrs" class="bg-teal-500 px-4 py-2 font-bold text-white">
            Open tooltip
          </button>
        </template>

        This is my message tooltip
      </v-tooltip>
    </div>
  </div>
</template>
