<template>
  <div>
    <div class="col-12">
      <div class="card">
        <div class="card-header d-flex flex-column">
          <h3 class="card-title">Davetli Listesi</h3>
          <div class="flex justify-content-between w-full">
            <div class="btn-list w-full">
              <TableControls
                  :searchQuery="searchQuery"
                  @search="searchData"
                  @add="openDialog"
              />
            </div>
          </div>
        </div>

        <DataTable
            :headers="headers"
            :items="paginatedData"
            :sortColumn="sortColumn"
            :sortDirection="sortDirection"
            @sort="sortBy"
            :slug="route.params.slug"
        />
      </div>
    </div>
    <div class="mt-4 flex items-center justify-between">
      <div>
        <span class="text-sm text-gray-700">
          Gösterilen {{ startIndex + 1 }} - {{ endIndex }} / {{ filteredData.length }}
        </span>
      </div>
      <div>
        <nav class="relative z-0 inline-flex rounded-md shadow-sm -space-x-px" aria-label="Pagination">
          <button
              @click="prevPage"
              :disabled="currentPage === 1"
              class="relative inline-flex items-center px-2 py-2 rounded-l-md border border-gray-300 bg-white text-sm font-medium text-gray-500 hover:bg-gray-50"
          >
            Önceki
          </button>
          <button
              @click="nextPage"
              :disabled="currentPage === totalPages"
              class="relative inline-flex items-center px-2 py-2 rounded-r-md border border-gray-300 bg-white text-sm font-medium text-gray-500 hover:bg-gray-50"
          >
            Sonraki
          </button>
        </nav>
      </div>
    </div>
    <div v-if="showDialog" class="fixed inset-0 bg-black bg-opacity-50 flex items-center justify-center">
      <div class="bg-white p-6 rounded-lg shadow-xl w-1/2">
        <h2 class="text-xl font-bold mb-4">Davetli Ekle</h2>
        <form @submit.prevent="addNewData">
          <div v-for="header in headers" :key="header" class="mb-4">
            <label :for="headerToKey(header)" class="block text-sm font-medium text-gray-700 mb-1">{{ header }}</label>
            <input
                :id="headerToKey(header)"
                v-model="newData[headerToKey(header)]"
                class="w-full border border-gray-300 px-3 py-2 rounded-md focus:outline-none focus:ring-2 focus:ring-blue-500"
                required
            />
          </div>
          <div class="flex justify-end">
            <button
                type="button"
                @click="closeDialog"
                class="mr-2 px-4 py-2 border border-gray-300 rounded-md text-sm font-medium text-gray-700 hover:bg-gray-50 focus:outline-none focus:ring-2 focus:ring-offset-2 focus:ring-blue-500"
            >
              İptal
            </button>
            <button
                type="submit"
                class="px-4 py-2 bg-blue-500 text-white rounded-md text-sm font-medium hover:bg-blue-600 focus:outline-none focus:ring-2 focus:ring-offset-2 focus:ring-blue-500"
            >
              Ekle
            </button>
          </div>
        </form>
      </div>
    </div>
  </div>
</template>

<script setup>
import {ref, computed, onMounted, watch} from 'vue'
import {useRoute} from 'vue-router'
import DataTable from '/components/dataTable/dataTable.vue'
import TableControls from '/components/tableControls/tableControls.vue'

const headers = ['Ad-Soyad', 'Masa Numarası', 'Masa Kişi Sayısı']

const data = ref([])
const searchQuery = ref('')
const showDialog = ref(false)
const newData = ref({})
const sortColumn = ref('name')
const sortDirection = ref('asc')
const currentPage = ref(1)
const itemsPerPage = 10

const headerToKey = (header) => {
  const map = {
    'Ad-Soyad': 'name',
    'Masa Numarası': 'tableNumber',
    'Masa Kişi Sayısı': 'peopleAtTable'
  }
  return map[header] || header.toLowerCase().replace(/\s+/g, '_')
}

const route = useRoute()

const fetchData = async () => {
  try {
    const response = await fetch('/data/events.json') // Replace with the correct path
    const json = await response.json()

    // Find the event that matches the current route's slug
    const event = json.events.find(event => event.slug === route.params.slug)
    if (event) {
      data.value = event.attendees
    } else {
      console.error('Event not found')
    }
  } catch (error) {
    console.error('Error fetching data:', error)
  }
}

// Re-fetch data whenever the route changes (for example, when navigating to a different event)
watch(() => route.params.slug, fetchData)

onMounted(() => {
  fetchData()
})

const filteredData = computed(() => {
  let result = data.value
  if (searchQuery.value) {
    const query = searchQuery.value.toLowerCase()
    result = result.filter(item =>
        Object.values(item).some(val =>
            val.toString().toLowerCase().includes(query)
        )
    )
  }
  return result.sort((a, b) => {
    const aValue = a[sortColumn.value]
    const bValue = b[sortColumn.value]
    if (aValue < bValue) return sortDirection.value === 'asc' ? -1 : 1
    if (aValue > bValue) return sortDirection.value === 'asc' ? 1 : -1
    return 0
  })
})

const paginatedData = computed(() => {
  const start = (currentPage.value - 1) * itemsPerPage
  const end = start + itemsPerPage
  return filteredData.value.slice(start, end)
})

const totalPages = computed(() => Math.ceil(filteredData.value.length / itemsPerPage))
const startIndex = computed(() => (currentPage.value - 1) * itemsPerPage)
const endIndex = computed(() => Math.min(startIndex.value + itemsPerPage, filteredData.value.length))

const searchData = (query) => {
  searchQuery.value = query
  currentPage.value = 1
}

const sortBy = (column) => {
  const mappedColumn = headerToKey(column)
  if (sortColumn.value === mappedColumn) {
    sortDirection.value = sortDirection.value === 'asc' ? 'desc' : 'asc'
  } else {
    sortColumn.value = mappedColumn
    sortDirection.value = 'asc'
  }
}

const prevPage = () => {
  if (currentPage.value > 1) {
    currentPage.value--
  }
}

const nextPage = () => {
  if (currentPage.value < totalPages.value) {
    currentPage.value++
  }
}

const openDialog = () => {
  showDialog.value = true
}

const closeDialog = () => {
  showDialog.value = false
}

const addNewData = () => {
  data.value.push({...newData.value})
  closeDialog()
}
</script>

<style lang="scss" scoped></style>
