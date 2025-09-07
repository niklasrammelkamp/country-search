<script setup lang="ts">
import type { CountryPicker } from '@yusifaliyevpro/countries/types'
import ListItem from './listItem/ListItem.vue'

export interface CustomCountriesType {
  items: CountryPicker<('name' | 'flag' | 'capital' | 'population' | 'region')[]>[]
}

defineProps<{
  items: CustomCountriesType['items']
}>()
</script>

<template>
  <section class="list-section">
    <ul class="list">
      <ListItem v-for="(item, index) in items" :key="index" :item="item" />
    </ul>
  </section>
</template>

<style scoped>
.list-section {
  margin-top: 1rem;
  max-width: 500px;
  margin: 0 auto;
}

.list {
  list-style: none;
  padding: 0;
  margin: 0;
}
</style>
