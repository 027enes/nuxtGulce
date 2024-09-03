<template>
  <div>
    <p v-if="error">Error: {{ error.message }}</p>
    <div v-else-if="event">


      <div class="page-wrapper">
        <!-- Page header -->
        <div class="page-header d-print-none">
          <div class="container-xl">
            <div class="row g-2 align-items-center">
              <div class="col">
                <h2 class="page-title">
                  {{ event.eventName }}
                </h2>
              </div>
            </div>
          </div>
        </div>
        <!-- Page body -->
        <div class="page-body">
          <div class="container-xl">
            <div class="row row-deck row-cards">
              <EventStatisticsCard />
              <wedding-table />
            </div>
          </div>
        </div>


      </div>


    </div>
    <p v-else>Loading...</p>

  </div>



</template>

<script setup>
import {ref, computed} from 'vue';
import {useRoute} from 'vue-router';
import {useFetch} from '@vueuse/core';
import EventStatisticsCard from "~/components/eventStatisticsCard/eventStatisticsCard.vue";
import WeddingTable from "~/components/weddingTable/weddingTable.vue";

const route = useRoute();
const slug = computed(() => route.params.slug);
const {data: eventsData, error} = useFetch('/data/events.json').json();

const event = computed(() => {
  if (eventsData.value) {
    return eventsData.value.events.find((item) => String(item.slug) === String(slug.value)) || null;
  }
  return null;
});

</script>

<style lang="scss" scoped>
</style>
