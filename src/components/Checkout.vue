<script setup lang="ts">
import { computed } from "vue";
import { Show } from "../shared/types";

const props = defineProps<{ shows: Show[] }>();

const Order_Fee = 8.0;
const Service_Fee = 12;

const showCart = computed(() => {
  return props.shows.filter((show) => show.count > 0);
});

const hasItems = computed(() => {
  return showCart.value.length > 0;
});

const subTotal = computed(() => {
  return showCart.value.reduce((total, show) => {
    return total + show.price * show.count;
  }, 0);
});

const tax = computed(() => {
  return (subTotal.value * Order_Fee) / 100;
});

const total = computed(() => {
  return subTotal.value + tax.value + Service_Fee;
});
</script>

<template>
  <div class="p-3">
    <h2 class="font-bold">CHECKOUT <i class="bi bi-cart3"></i></h2>
    <div class="flex flex-col" v-if="hasItems">
      <div class="mt-3">
        <h3 class="text-xl font-bold">Tickets</h3>
        <ul>
          <li v-for="show in showCart" :key="show.id" class="">
            <span>{{ show.title }} (Qty. {{ show.count }})</span>
            <span class="float-right"
              >${{ (show.price * show.count).toFixed(2) }}</span
            >
          </li>
        </ul>
      </div>
      <div class="mt-3">
        <h3 class="text-xl font-bold">Fees</h3>
        <ul>
          <li>
            <span>Service Fee</span>
            <span class="float-right">Ksh 9.00</span>
          </li>
          <li>
            <span>Tax ({{ Order_Fee }}%)</span>
            <span class="float-right">Ksh{{ tax.toFixed(2) }}</span>
          </li>
        </ul>
      </div>

      <div class="mt-3 text-xl font-bold">
        <h3 class="grow inline">TOTAL</h3>
        <span class="float-right">Ksh{{ total.toFixed(2) }}</span>
      </div>

      <div class="mt-3">
        <h3 class="font-bold">Note</h3>
        <p>
          *All sales are Final - No Refund
        </p>
      </div>
      <button type="submit" class="bg-green-800 mt-3 py-3 px-12 rounded-lg">
        Place Order
      </button>
    </div>
    <div class="text-center mx-auto py-4" v-else>
      Please add some tickets to your cart to checkout!
    </div>
  </div>
</template>

<style scoped>
</style>