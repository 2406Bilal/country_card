<template>
  <RouterLink
    :to="{
      name: 'country',
      params: {
        name: item.name.common,
      },
    }"
  >
    <div
      class="inline-block p- ml-3 mt-3 h-80 border-8 w-60 place-items-center  "
    >
      <div class="w-full h-52 object-cover ">
        <img :src="item.flags.png" alt="" />
      </div>
      <h2>name: {{ item.name.common }}</h2>
      <h2>capital: {{ item.capital ? item.capital[0] : "" }}</h2>
      <h2>population: {{ item.population }}</h2>
    </div>
  </RouterLink>
</template>

<script setup>
import { defineProps } from "vue";
import { RouterLink } from "vue-router";

const props = defineProps({
  item: {
    type: [Object, Array],
    required: true,
  },
});
</script>
