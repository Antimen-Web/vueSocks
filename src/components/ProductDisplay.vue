<script setup>
import { computed, ref } from "vue";
import ReviewForm from "@/components/ReviewForm.vue";
import ReviewList from "@/components/ReviewList.vue";

const props = defineProps({
  premium: {
    type: Boolean,
    required: true,
  },
});

const product = "Socks";
const brand = "Antimen-Web";
const details = ["50% cotton", "30% wool", "20% polyester"];
const variants = [
  {
    id: 2234,
    color: "green",
    image: "src/assets/images/socks_green.jpg",
    quantity: 50,
  },
  {
    id: 2235,
    color: "blue",
    image: "src/assets/images/socks_blue.jpg",
    quantity: 0,
  },
];

const title = computed(() => {
  return brand + " " + product;
});
const selectedVariant = ref(0);
const image = computed(() => {
  return variants[selectedVariant.value].image;
});
const inventory = computed(() => {
  return variants[selectedVariant.value].quantity;
});
const shipping = computed(() => {
  if (props.premium) {
    return "Free";
  }
  return 2.99;
});

const reviews = ref([]);
</script>

<template>
  <div class="product-display">
    <div class="product-container">
      <div class="product-image">
        <img :src="image" :alt="product" />
      </div>
      <div class="product-info">
        <h1>{{ title }}</h1>
        <p v-if="inventory > 10">In Stock</p>
        <p v-else-if="inventory <= 10 && inventory > 0">Almost Out Stock</p>
        <p v-else>Out Stock</p>
        <p>Shipping: {{ shipping }}</p>
        <ul>
          <li v-for="detail in details">{{ detail }}</li>
        </ul>
        <div
          v-for="(variant, index) in variants"
          :key="variant.id"
          @mouseover="() => (selectedVariant = index)"
          class="color-circle"
          :style="{ background: variant.color }"
        ></div>
        <button
          class="button"
          :class="{ disabledButton: !inventory }"
          :disabled="!inventory"
          @click="() => $emit('add-to-cart', variants[selectedVariant].id)"
        >
          Add to Cart
        </button>
      </div>
    </div>
    <review-list v-if="reviews.length" :reviews="reviews"></review-list>
    <review-form
      @review-submitted="(review) => reviews.push(review)"
    ></review-form>
  </div>
</template>

<script>
export default {
  name: "ProductDisplay",
};
</script>
