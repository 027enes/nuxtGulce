<template>
  <div class="bg-white shadow-md rounded-lg overflow-hidden">
    <table class="w-full">
      <thead>
      <tr class="bg-gray-50 border-b-2 text-left text-xs font-medium text-gray-500 uppercase tracking-wider text-center">
        <th
            v-for="header in headers"
            :key="header"
            @click="$emit('sort', header)"
            class="px-6 py-3 cursor-pointer hover:bg-gray-100 text-center"
        >
          {{ header }}
          <span v-if="sortColumn === headerToKey(header)">
              {{ sortDirection === 'asc' ? '▲' : '▼' }}
            </span>
        </th>
        <th>
          Durumu
        </th>
      </tr>
      </thead>
      <tbody class="bg-white divide-y divide-gray-200">
      <tr v-for="item in items" :key="item.id" class="hover:bg-gray-50">
        <td v-for="header in headers" :key="header" class="px-6 py-4 whitespace-nowrap text-center">
          {{ item[headerToKey(header)] }}
        </td>
        <td class="px-6 py-4 whitespace-nowrap text-center d-flex justify-center">
          <button class="bg-red-500 hover:bg-red-400 h-5 w-5 d-block rounded">
            <nuxt-link :to="`/events/${slug}/${item.name}`" class="w-full h-full d-flex items-center p-1 justify-center">
              <ScanSearch class="text-white hover:text-black h-4 w-4"/>
            </nuxt-link>
          </button>
        </td>
      </tr>
      </tbody>
    </table>
  </div>
</template>

<script setup>
import { ScanSearch } from 'lucide-vue-next';
import { defineProps, defineEmits } from 'vue';

const props = defineProps({
  headers: {
    type: Array,
    required: true,
  },
  items: {
    type: Array,
    required: true,
  },
  sortColumn: {
    type: String,
    required: true,
  },
  sortDirection: {
    type: String,
    required: true,
  },
  slug: {
    type: String,
    required: true,
  }
})

const headerToKey = (header) => {
  const map = {
    'Ad-Soyad': 'name',  // Assuming 'name' is the key in your items array
    'Masa Numarası': 'tableNumber',  // Assuming 'tableNumber' is the key in your items array
    'Masa Kişi Sayısı': 'peopleAtTable',  // Assuming 'peopleAtTable' is the key in your items array
  }
  return map[header] || header.toLowerCase().replace(/\s+/g, '_')
}

defineEmits(['sort'])
</script>

<style scoped>
</style>
