<template>
  <div
    class="w-3/5 m-auto mt-10 ml-8 flex  center bg-clip-content border-4 border-neutral-950 border-dashed content-evenly"
  >
    <div class="w-64">
      <img :src="country?.flags?.svg" alt="" />
    </div>
    <div class="text-black-500 font-xl font-mono ml-4">
      <strong>name:{{ country?.name?.official }}</strong>
      <h1>population:{{ country?.population }}</h1>
      <h1>region:{{ country?.region }}</h1>
      <h1>capital:{{ country?.capital }}</h1>
    </div>
  </div>
</template>

<script setup>
import { defineProps, onMounted, ref, watchEffect } from "vue";

const props = defineProps({
  name: String,
});

const country = ref({});

onMounted(() => {
  fetch(`https://restcountries.com/v3.1/name/${props.name}`)
    .then((response) => response.json())
    .then((data) => {
      country.value = data[0];
    });
});

watchEffect(() => {
  console.log(country.value);
});
</script>
