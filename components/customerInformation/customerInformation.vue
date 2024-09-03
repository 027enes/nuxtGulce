<template>
  <div class="card">

    <div class="card-header">
      <h3 class="card-title">Kişisel Bilgiler</h3>
    </div>

    <div class="card-body">
      <div class="datagrid">
        <div class="datagrid-item ">
          <div class="datagrid-title">İsim Soyisim</div>
          <div class="datagrid-content">
            <div class="d-flex align-items-center">
            <span class="avatar avatar-xs me-2 rounded"
                  :style="{ backgroundImage: `url('https://ui-avatars.com/api/?background=0D8ABC&color=fff&name=${encodeURIComponent(attendee.name)}')`}">
            </span>
            {{ attendee.name }}
            </div>
          </div>
        </div>
        <div class="datagrid-item d-flex items-center flex-col">
          <div class="datagrid-title">Telefon Numarası</div>
          <div class="datagrid-content">{{ attendee.phoneNumber }}</div>
        </div>
        <div class="datagrid-item d-flex items-center flex-col">
          <div class="datagrid-title">Masa Numarası</div>
          <div class="datagrid-content">{{ attendee.tableNumber }}</div>
        </div>
        <div class="datagrid-item d-flex items-center flex-col">
          <div class="datagrid-title">Katılacak Sayısı</div>
          <div class="datagrid-content">
            <span class="status status-green">{{ attendee.peopleAtTable }}</span>
          </div>
        </div>
        <div class="datagrid-item d-flex items-center flex-col">
          <div class="datagrid-title">Durum</div>
          <div class="datagrid-content">
            <svg xmlns="http://www.w3.org/2000/svg" class="icon text-green" width="24" height="24"
                 viewBox="0 0 24 24" stroke-width="2" stroke="currentColor" fill="none" stroke-linecap="round"
                 stroke-linejoin="round">
              <path stroke="none" d="M0 0h24v24H0z" fill="none"/>
              <path d="M5 12l5 5l10 -10"/>
            </svg>
          </div>
        </div>
      </div>
    </div>
  </div>

</template>

<script setup>
const props = defineProps({
  attendee: Object
});
</script>

<style lang="scss" scoped>

</style>