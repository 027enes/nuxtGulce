<template>
  <div class="col-12">
    <div class="card mt-6">
      <div class="card-header">
        <h3 class="card-title">Masadaki Diğer Davetliler</h3>
      </div>
      <div class="card-body">
        <div class="row g-3">
          <!-- Loop through each guest to display their details -->
          <div class="col-3" v-for="guest in guests" :key="guest.name">
            <div class="row g-3 align-items-center">
              <a href="#" class="col-auto">
              <span
                  class="avatar"
                  :style="{ backgroundImage: `url('https://ui-avatars.com/api/?background=0D8ABC&color=fff&name=${encodeURIComponent(guest.name)}')` }"
              ></span>
              </a>
              <div class="col text-truncate">
                <nuxt-link :to="`/events/${slug}/${guest.name}`" class="text-reset d-block text-truncate">{{ guest.name }}</nuxt-link>
                <div class="text-secondary text-truncate mt-n1">Masa {{ guest.tableNumber }}</div>
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script setup>
import { defineProps } from 'vue';

// Define the `guests` prop properly as an array of objects
const props = defineProps({
  guests: {
    type: Array,
    required: true,
    default: () => []
  },
  slug: {
    type: String,
    required: true
  }
});
</script>

<style lang="scss" scoped>
</style>
