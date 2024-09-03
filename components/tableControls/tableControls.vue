<template>
  <div class="mb-4 d-flex justify-between items-center w-full">
    <div class="relative">
      <input
          :value="searchQuery"
          @input="$emit('search', $event.target.value)"
          class="pl-10 pr-4 py-2 border rounded-md focus:outline-none focus:ring-2 focus:ring-blue-500"
          placeholder="Ara..."
      />
      <div class="absolute inset-y-0 left-0 pl-3 flex items-center pointer-events-none">
        <svg
            class="h-5 w-5 text-gray-400"
            fill="none"
            stroke="currentColor"
            viewBox="0 0 24 24"
            xmlns="http://www.w3.org/2000/svg"
        >
          <path
              stroke-linecap="round"
              stroke-linejoin="round"
              stroke-width="2"
              d="M21 21l-6-6m2-5a7 7 0 11-14 0 7 7 0 0114 0z"
          ></path>
        </svg>
      </div>
    </div>
    <div class="flex gap-2">
      <Export class="btn" />
      <button
          @click="$emit('add')"
          class="bg-blue-500 text-white px-4 py-2 rounded-sm hover:bg-blue-600 focus:outline-none focus:ring-2 focus:ring-blue-500 focus:ring-offset-2"
      >
        Davetli Ekle
      </button>
    </div>
  </div>
</template>

<script setup>
import Export from '@/components/export/export.vue';

defineProps({
  searchQuery: {
    type: String,
    required: true,
  },
});

defineEmits(['search', 'add']);
</script>

<style scoped></style>
