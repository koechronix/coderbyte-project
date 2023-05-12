<script setup lang="ts">
import { computed, ref } from "vue";
import ShowListItem from "./components/ShowListItem.vue";
import PaymentCheckoutForm from "./components/PaymentCheckoutForm.vue";

const shows = ref([
  {
    id: 1,
    title: "The Way to Power",
    subtitle: "By kelly Foundation.",
    location: "Nyayo,Nairobi",
    price: 300,
    count: ref(0),
  },
  {
    id: 2,
    title: "Hyper Focus",
    subtitle: "By Divyshan Foundations.",
    location: "Kasarani,Nairobi",
    price: 400,
    count: ref(0),
  },
  {
    id: 3,
    title: "Intelligent Investor",
    subtitle: "By Ronix Foundations",
    location: "Tamasha,Nairobi",
    price: 250,
    count: ref(0),
  },
  {
    id: 4,
    title: "Atomic Habits",
    subtitle: "By Clear Foundations",
    location: "Jogoo, Nairobi",
    price: 500,
    count: ref(0),
  },
  {
    id: 5,
    title: "Psychology Of Persuation",
    subtitle:"By Robert Foundations",
    location: "Ruiru,Nairobi",
    price: 500,
    count: ref(0),
  },
  
]);

const totalCount = computed(() => {
  return shows.value.reduce((prev, show) => {
    return prev + show.count;
  }, 0);
});
</script>

<template>
  <header class="flex row">
    <nav class="flex-grow">
      <h1 class="text-xl inline" role="button">
        <a href="/">Ticket Master</a>
      </h1>
    </nav>
    <div>
      <span class="mr-2">{{ totalCount }}</span>
      <i class="bi bi-cart2 text-xl"></i>
    </div>
  </header>
  <div class="mt-8">
    <h2 class="font-bold mb-2">
      Upcoming Shows <i class="bi bi-calendar2-plus-fill"></i>
    </h2>
    <ul class="grid grid-cols-1 md:grid-cols-2 gap-x-5 gap-y-3">
      <ShowListItem
        v-for="show in shows"
        :key="show.id"
        :show="show"
      ></ShowListItem>
    </ul>
  </div>
  <div class="mt-8">
    <PaymentCheckoutForm :shows="shows" />
  </div>
</template>

<style scoped>
</style>
