<script setup lang="ts">
import { ref } from 'vue'
import CountryList from './countrySearch/CountryList.vue'
import type { CustomCountriesType } from './countrySearch/CountryList.vue'
import { getCountriesByName } from '@yusifaliyevpro/countries'

// Reaktive Variablen
const searchQuery = ref('')
const countries = ref<CustomCountriesType['items']>([])
const loading = ref(false)
const error = ref<string | null>(null)

const fetchCountries = async () => {
  error.value = null
  loading.value = true

  if (searchQuery.value.trim() === '') {
    countries.value = []
    loading.value = false
    return
  }

  const data = await getCountriesByName({
    name: searchQuery.value,
    fields: ['name', 'flag', 'capital', 'population', 'region'],
  })
  console.log('data', data)

  if (!data) {
    error.value = 'Keine Länder gefunden'
    countries.value = []
    return
  }

  countries.value = data ?? []
  loading.value = false
}

// watch(countries, (newVal) => {
//   console.log('countries', newVal)
// })
</script>

<template>
  <section class="section">
    <h1 class="headline">Länder Browser</h1>

    <p class="description">
      Suche nach Ländern, um Informationen wie Hauptstadt, Bevölkerung und Region zu erhalten.
    </p>

    <input
      class="input"
      v-model="searchQuery"
      type="text"
      placeholder="Länder suchen..."
      @input="fetchCountries"
      name="country-search"
    />

    <div v-if="loading">⏳</div>
    <div v-else-if="error">⚠️ {{ error }}</div>
  </section>

  <CountryList v-if="countries.length != 0" :items="countries" />
</template>

<style scoped>
.section {
  display: flex;
  flex-direction: column;
  max-width: 500px;
  margin: 0 auto;
}

.headline {
  font-size: 2rem;
  font-weight: bold;

  text-align: center;
}

.description {
  opacity: 0.7;
  text-align: center;
}

.input {
  padding: 0.5rem 1rem;
  border: 1px solid #ccc;
  border-radius: 4px;
  font-size: 1rem;
  margin-top: 3rem;
}
</style>
