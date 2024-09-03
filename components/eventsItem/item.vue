<template>
  <div class="col-sm-6 col-lg-3">
    <nuxt-link :to="`/events/${slug}`" class="card">
      <div class="card-body">
        <div class="d-flex align-items-center">
          <h2 class="h1">{{ weddingTitle }}</h2>
        </div>
        <div class="d-flex flex-column mb-2 gap-1">
          <div>{{ weddingType }}</div>
          <div class="d-flex align-items-center gap-1">
            <span>{{weddingLocation}}</span>
          </div>
          <div class="d-flex align-items-center gap-1">
            <span>{{weddingTime}}</span>
          </div>
        </div>
      </div>
    </nuxt-link>
  </div>
</template>

<script setup>
import {defineProps} from "vue";
const props = defineProps({
  weddingTitle:{type: String, required: true},
  weddingType:{type: String, required: true},
  weddingTime:{type: String, required: true},
  weddingLocation:{type: String, required: true},
  slug:{type: String, required: true}
});
</script>

<style lang="scss" scoped>

</style>