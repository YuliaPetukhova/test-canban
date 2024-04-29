<template>
  <div class="rating-panel">
    <v-tooltip text="Сортировка по возрастанию рейтинга">
      <template v-slot:activator="{ props }">
        <v-btn
            v-bind="props"
            icon="mdi-sort-ascending"
            density="compact"
            variant="tonal"
            class="rating-btn"
            color="white"
            @click="sortAscRating"/>
      </template>
    </v-tooltip>

    <v-tooltip text="Сортировка по убыванию рейтинга">
      <template v-slot:activator="{ props }">
        <v-btn
            v-bind="props"
            icon="mdi-sort-descending"
            density="compact"
            variant="tonal"
            class="rating-btn"
            color="white"
            @click="sortDescRating"/>
      </template>
    </v-tooltip>

    <v-tooltip text="Без сортировки">
      <template v-slot:activator="{ props }">
        <v-btn
            v-bind="props"
            icon="mdi-sort-variant-off"
            density="compact"
            variant="tonal"
            class="rating-btn"
            color="white"
            @click="resetSortList"/>
      </template>
    </v-tooltip>
  </div>
</template>

<script setup>
import {ref, inject} from 'vue';

const firstList = inject('firstList');
const secondList = inject('secondList');
const lastList = inject('lastList');

let cards = ref([]);

const props = defineProps({
  options: {},
});

function getLocalCards() {
  switch (props.options.id) {
    case 1:
      cards = firstList;
      break;
    case 2:
      cards = secondList;
      break;
    case 3:
      cards = lastList;
      break;
  }
}

function sortDescRating() {
  getLocalCards();
  cards = cards.value.sort((a, b) => b.rating.rate - a.rating.rate);
}

function sortAscRating() {
  getLocalCards();
  cards = cards.value.sort((a, b) => a.rating.rate - b.rating.rate);
}

function resetSortList() {
  getLocalCards();
  cards = cards.value.sort((a, b) => a.id - b.id);
}
</script>


<style scoped lang="scss">
.rating-panel {
  border: 2px solid #fff;
  border-radius: 10px;
  padding: 10px 0;
  display: flex;
  justify-content: space-around;
}
</style>