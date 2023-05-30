<script setup lang="ts">
import { Show } from "../shared/types";

const props = defineProps<{ show: Show }>();

const incrementCount = () => {
  props.show.count++;
};

const decrementCount = () => {
  if (props.show.count === 0) return;
  props.show.count--;
};
</script>

<template>
  <li class="flex flex-row bg-stone-600 rounded-md p-2">
    <div class="flex-grow">
      <h2 class="text-lg">
        {{ show.title
        }}<span class="ml-2 text-sm text-red-300"
          >({{ show.location }})</span
        >
      </h2>
      <p class="text-green-400">{{ show.subtitle }}</p>
    </div>
    <div class="flex flex-col">
      <div class="text-center">${{ show.price.toFixed(2) }}</div>
      <div class="text-center">
        <button @click="decrementCount">
          <i class="bi bi-dash-square"></i>
        </button>
        {{ show.count }}
        <button @click="incrementCount">
          <i class="bi bi-plus-square"></i>
        </button>
      </div>
    </div>
  </li>
</template>

<style scoped>
</style>


