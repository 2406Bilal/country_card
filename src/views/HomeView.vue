<template>
  <div>
    <label class="block">
      <span class="text-gray-700">enter name of the country</span>
      <input
        type="text"
        v-model="search"
        class="mt-1 block rounded-md w-full border-gray-300 shadow-sm focus:border-indigo-300 focus:ring focus:ring-indigo-200 focus:ring-opacity-50 caret-pink-500"
        placeholder="enter here"
      />
    </label>
    <!-- <select v-model="selectedRegion">
      <option value="europe">Europe</option>
      <option value="americas">America</option>
      <option value="asia">Asia</option>
    </select> -->
    <label class="block">
      <span class="text-gray-700">choose your ragion:</span>
      <select
        v-model="selectedRegion"
        class="block w-full mt-1 rounded-md border-gray-300 shadow-sm focus:border-indigo-300 focus:ring focus:ring-indigo-200 focus:ring-opacity-50"
      >
        <option value="">regions</option>
        <option value="europe">Europe</option>
        <option value="americas">America</option>
        <option value="asia">Asia</option>
        >
      </select>
    </label>
  </div>
  <div>
    <ItemCard v-for="(item, key) in filteredItems" :key="key" :item="item" />
  </div>
</template>

<script setup>
import { ref, onMounted, computed, watchEffect } from "vue";
import ItemCard from "./ItemComponent.vue";

const items = ref([]);
const search = ref("");
const selectedRegion = ref("");

function getCountries() {
  fetch("https://restcountries.com/v3.1/all")
    .then((response) => response.json())
    .then((data) => {
      items.value = data;
    });
}

onMounted(() => {
  getCountries()
});

const filteredItems = computed(() => {
  if (search.value || !!items.length) {
    return items.value.filter((item) => {
      return item.name.common
        .toLowerCase()
        .includes(search.value.toLowerCase());
    });
  } else {
    return items.value;
  }
});

watchEffect(() => {
  if (selectedRegion.value) {
    fetch(`https://restcountries.com/v3.1/region/${selectedRegion.value}`)
      .then((response) => response.json())
      .then((data) => {
        items.value = data;
      });
  } else {
    getCountries()
  }
});
</script>

<style>
body {
  display: inline-block;
}
</style>
