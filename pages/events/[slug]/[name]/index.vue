<template>
  <div>
    <Header/>
    <div>

      <div class="page-wrapper">
        <!-- Page header -->
        <div class="page-header d-print-none">
          <div class="container-xl">
            <div class="row g-2 align-items-center">
              <div class="col">
                <h2 class="page-title">
                  {{ eventAndAttendee.event?.eventName }}
                </h2>
              </div>
              <div class="col-auto ms-auto d-print-none">
                <div class="btn-list">
                            <span class="d-none d-sm-inline">
                              <a href="#" class="btn">
                                Yazdır
                              </a>
                            </span>
                  <nuxt-link to="/" class="btn btn-primary d-flex" data-bs-toggle="modal"
                     data-bs-target="#modal-report">
                    <svg xmlns="http://www.w3.org/2000/svg" class="icon" width="24" height="24" viewBox="0 0 24 24"
                         stroke-width="2" stroke="currentColor" fill="none" stroke-linecap="round"
                         stroke-linejoin="round">
                      <path stroke="none" d="M0 0h24v24H0z" fill="none"/>
                      <path d="M12 5l0 14"/>
                      <path d="M5 12l14 0"/>
                    </svg>
                    Sms Gönder
                  </nuxt-link>
                </div>
              </div>

            </div>
          </div>
        </div>
        <!-- Page body -->
        <div class="page-body">
          <div class="container-xl">
            <div v-if="error">
              <p>Error: {{ error.message }}</p>
            </div>
            <div v-else-if="attendee">
              <CustomerInformation :attendee="attendee"/>
            </div>
            <otherGuests :guests="guests" :slug="slug"/>
          </div>
        </div>
      </div>
    </div>
    <Footer/>
  </div>
</template>

<script setup>
import Header from "~/components/header/header.vue";
import Footer from '~/components/footer/footer.vue';
import otherGuests from '~/components/otherGuests/otherGuests.vue';
import CustomerInformation from '~/components/customerInformation/customerInformation.vue';
import {ref, computed} from 'vue';
import {useRoute} from 'vue-router';
import {useFetch} from '@vueuse/core';

const route = useRoute();
const name = computed(() => route.params.name);  // Get the attendee's name from the route

const {data: customer, error} = useFetch('/data/events.json').json();

const attendee = computed(() => {
  if (customer.value) {
    for (let event of customer.value.events) {
      const foundAttendee = event.attendees.find(a => a.name === name.value);
      if (foundAttendee) {
        return foundAttendee;
      }
    }
  }
  return null;
});

const eventAndAttendee = computed(() => {
  if (customer.value) {
    for (let event of customer.value.events) {
      const foundAttendee = event.attendees.find(a => a.name === name.value);
      if (foundAttendee) {
        return { event, attendee: foundAttendee };
      }
    }
  }
  return { event: null, attendee: null };
});

const guests = computed(() => {
  if (eventAndAttendee.value.event) {
    return eventAndAttendee.value.event.attendees.filter(a => a.name !== eventAndAttendee.value.attendee.name);
  }
  return [];
});

const slug = computed(() => route.params.slug);
</script>

<style lang="scss" scoped></style>
