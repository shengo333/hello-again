<template>
  <div class="filter-wrapper">
    <div>
      <p>select filter condition</p>

      <select v-model="selectedFilter" @change="addFilter">
        <option v-for="filter in filters" :value="filter" :key="filter">
          {{ filter }}
        </option>
      </select>
    </div>
    <div
      v-for="(filter, index) in selectedFilters"
      :key="index"
      class="option-wrapper"
    >
      <!-- Inputs for selected filters -->
      <div v-if="filter === 'Activity'" class="filter-options">
        <p>{{ filter }}</p>
        <input
          type="text"
          :placeholder="filter.toLowerCase()"
          v-model="filterValues[filter]"
          @input="emitFilter"
        />
        <button @click="deleteFilter(filter)">Delete</button>
      </div>
      <div v-if="filter === 'Last purchase'" class="filter-options">
        <p>{{ filter }}</p>

        <input
          type="text"
          :placeholder="filter.toLowerCase()"
          v-model="filterValues[filter]"
          @input="emitFilter"
        />
        <button @click="deleteFilter(filter)">Delete</button>
      </div>
      <div v-if="filter === 'Segment'" class="filter-options">
        <p>{{ filter }}</p>

        <input
          type="text"
          :placeholder="filter.toLowerCase()"
          v-model="filterValues[filter]"
          @input="emitFilter"
        />
        <button @click="deleteFilter(filter)">Delete</button>
      </div>
      <div v-if="filter === 'Email'" class="filter-options">
        <p>{{ filter }}</p>

        <input
          type="text"
          :placeholder="filter.toLowerCase()"
          v-model="filterValues[filter]"
          @input="emitFilter"
        />
        <button @click="deleteFilter(filter)">Delete</button>
      </div>
    </div>

    <button @click="filterData" class="filter-data">Filter data</button>
  </div>
</template>

<script setup>
import { ref, reactive } from "vue";

const filters = ref(["Activity", "Last purchase", "Segment", "Email"]);
const selectedFilter = ref(null); // Initialize with null

// Input values for different selected filters
let filterValues = {}; // Initialize as an object

// Array to store selected filters
const selectedFilters = ref([]);

// Method to add selected filter to the array
const addFilter = () => {
  if (
    selectedFilter.value &&
    !selectedFilters.value.includes(selectedFilter.value)
  ) {
    selectedFilters.value.push(selectedFilter.value);
  }
};

const emit = defineEmits(["filterEmit"]);

// const emitFilter = () => {

//   emit("filterEmit", filterValues);
// };

function filterData() {
  emit("filterEmit", filterValues);
}

function deleteFilter(filter) {
  console.log(selectedFilters.value, "selected filers");

  selectedFilters.value = selectedFilters.value.filter(
    (selectedFilter) => selectedFilter !== filter
  );

  console.log(selectedFilters.value, "eeeeh");
}
</script>

<style scoped lang="scss">
.filter-wrapper {
  margin-top: 20px;
}

.filter-wrapper {
  display: flex;
  flex-direction: column;
  gap: 1rem;
}

.filter-options {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  gap: 2rem;
}

.filter-data {
  background: lightgreen;
  padding: 1rem;
  max-width: 10rem;
  border: none;
  border-radius: 15px;
}
</style>

