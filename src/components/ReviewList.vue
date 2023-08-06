<script setup>
const props = defineProps({
  reviews: {
    type: Array,
    required: true,
  },
});
</script>

<template>
  <div class="review-container">
    <h3>Reviews:</h3>
    <ul>
      <li v-for="(review, index) in props.reviews" :key="index">
        {{ review.name }} gave this {{ review.rating }} stars
        <br />
        "{{ review.review }}"
      </li>
    </ul>
  </div>
</template>

<script>
export default {
  name: "ReviewList",
};
</script>

<style scoped></style>
