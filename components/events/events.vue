<template>
  <div>

    <div class="page-wrapper">
      <!-- Page header -->
      <div class="page-header d-print-none">
        <div class="container-xl">
          <div class="row g-2 align-items-center">
            <div class="col">
              <h2 class="page-title">
                Etkinliklerimiz
              </h2>
            </div>
          </div>
        </div>
      </div>
      <!-- Page body -->
      <div class="page-body">
        <div class="container-xl">
          <div class="row row-deck row-cards">
            <events-item
                v-if="data && data.events"
                v-for="item in data.events"
                :key="item.eventName"
                :weddingTitle="item.eventName"
                :weddingType="item.eventType"
                :wedding-time="item.dateTime"
                :wedding-location="item.location"
                :slug="item.slug"
            />
          </div>
        </div>
      </div>


    </div>
  </div>
</template>

<script setup>
import EventsItem from "~/components/eventsItem/item.vue";
import {useFetch} from "@vueuse/core";

const {data, errors, pending} = useFetch('/data/events.json').json();
</script>

<style lang="scss" scoped>

</style>