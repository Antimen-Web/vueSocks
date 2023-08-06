<script setup>
import { ref } from "vue";
import ProductDisplay from "@/components/ProductDisplay.vue";

const cart = ref([]);
const premium = true;
</script>

<template>
  <div class="nav-bar"></div>

  <div class="cart">Cart({{ cart.length }})</div>

  <product-display
    :premium="premium"
    @add-to-cart="(id) => cart.push(id)"
  ></product-display>
</template>
