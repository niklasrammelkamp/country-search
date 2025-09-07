<script setup lang="ts">
import { ref } from 'vue'
import type { CustomCountriesType } from '../CountryList.vue'

defineProps<{
  item: CustomCountriesType['items'][0]
}>()

const showMore = ref(false)
</script>

<template>
  <li class="list-item">
    <!-- <details>
      <summary>
        <p>{{ item.flag }}</p>
        <p>{{ item.name.common }}</p>
      </summary>
      <p>Hauptstadt: {{ item.capital ? item.capital[0] : 'Keine Hauptstadt' }}</p>
      <p>Bevölkerung: {{ item.population.toLocaleString() }}</p>
      <p>Region: {{ item.region }}</p>
    </details> -->

    <button @click="showMore = !showMore" class="wrapper">
      <div class="summary">
        <p role="image" :aria-label="`Flagge von ${item.name.common}`">{{ item.flag }}</p>
        <h2 class="country-name">{{ item.name.common }}</h2>
      </div>

      <div v-if="showMore" class="details">
        <div class="detail-row">
          <p class="description">Hauptstadt:</p>
          <p class="result">{{ item.capital ? item.capital[0] : 'Keine Hauptstadt' }}</p>
        </div>

        <div class="detail-row">
          <p class="description">Bevölkerung:</p>
          <p class="result">{{ item.population.toLocaleString() }}</p>
        </div>

        <div class="detail-row">
          <p class="description">Region:</p>
          <p class="result">{{ item.region }}</p>
        </div>
      </div>
    </button>
  </li>
</template>

<style scoped>
.list-item {
  list-style: none;
  border-radius: 4px;
  margin-top: 1rem;
  background-color: #f9f9f9;
  transition: background-color 0.2s ease-in-out;

  .wrapper {
    display: flex;
    flex-direction: column;
    padding: 1rem;
    gap: 1rem;
    width: 100%;
    background: none;
    border: none;
    text-align: left;
    cursor: pointer;
    font-size: 1rem;
    color: var(--color-text);

    .summary {
      display: flex;
      align-items: center;
      gap: 1rem;

      .country-name {
        font-size: 1rem;
        margin: 0;
        font-weight: 600;
      }
    }

    .details {
      margin-top: 1rem;
      display: flex;
      flex-direction: column;
      gap: 0.5rem;

      .detail-row {
        display: flex;
        justify-content: space-between;
        margin-top: 0.5rem;

        .description {
          margin: 0;
        }

        .result {
          font-weight: 600;
          margin: 0;
        }
      }
    }
  }
}

.list-item:hover {
  background-color: #e0e0e0;
  cursor: pointer;
}
</style>
