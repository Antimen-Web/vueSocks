<script setup>
import { ref } from "vue";

const emit = defineEmits(["review-submitted"]);

let name = ref("");
let review = ref("");
let rating = ref(null);

let errors = ref({
  name: null,
  review: null,
  rating: null,
});

function validateForm() {
  errors.value = {};

  let isValid = true;

  if (!name.value) {
    errors.value.name = "Name is required";
    isValid = false;
  }

  if (!review.value) {
    errors.value.review = "Review is required";
    isValid = false;
  }

  if (rating.value === null) {
    errors.value.rating = "Rating is required";
    isValid = false;
  }

  return isValid;
}

function onSubmit() {
  if (!validateForm()) {
    return;
  }

  let productReview = {
    name: name.value,
    review: review.value,
    rating: rating.value,
  };
  emit("review-submitted", productReview);

  name.value = "";
  review.value = "";
  rating.value = null;
}
</script>

<template>
  <form class="review-form" @submit.prevent="onSubmit">
    <h3>Leave a review</h3>
    <label for="name">Name:</label>
    <input id="name" v-model="name" />
    <span class="error">{{ errors.name }}</span>

    <label for="review">Review:</label>
    <textarea id="review" v-model="review"></textarea>
    <span class="error">{{ errors.review }}</span>

    <label for="rating">Rating:</label>
    <select id="rating" v-model.number="rating">
      <option disabled value="">Select a rating</option>
      <option>5</option>
      <option>4</option>
      <option>3</option>
      <option>2</option>
      <option>1</option>
    </select>
    <span class="error">{{ errors.rating }}</span>

    <input class="button" type="submit" value="Submit" />
  </form>
</template>

<script>
export default {
  name: "ReviewForm",
};
</script>

<style scoped>
.error {
  color: red;
}
</style>
