<script setup>
import { ref, computed } from 'vue';

const sitename = ref("Vue.js Pet Depot");
const product = ref({
  id: 1234,
  title: "Cat Food, 25lb bag",
  description:
    "100 * 25 pound bag of <em>irresistible</em>, organic goodness for your cat.",
  price: 200000,
  image: "img/cat.jpg",
});
const count = ref(0);
// ADD YOUR CODE HERE

// Computed property: formats product.price (an integer number of cents)
// into a "$dollars.cents" string, e.g. 200000 -> "$2,000.00"
const calculated_price = computed(() => {
  const price = product.value.price;

  // Must be a positive integer, otherwise show nothing
  if (!Number.isInteger(price) || price <= 0) {
    return "";
  }

  const priceString = price.toString();
  const cents = priceString.slice(-2); // last 2 digits
  const dollars = priceString.slice(0, -2); // everything before that

  // toLocaleString() adds the comma separators for us, e.g. 2000 -> "2,000"
  const formattedDollars = Number(dollars).toLocaleString();

  return `$${formattedDollars}.${cents}`;
});

// Method: increments the cart count by 1 each time "Add to Cart" is clicked
function addToCart() {
  count.value++;
}

// Computed property: true once count reaches 10, used to disable the button
const cartFull = computed(() => count.value >= 10);

// END OF ADDING YOUR CODE HERE
</script>

<template>
  <!-- ADD OR MODIFY YOUR CODE HERE -->

  <div class="d-flex justify-content-between align-items-center">
    <h2 class="fs-2 mx-2">{{ sitename }}</h2>

    <!-- Shopping cart icon; https://icons.getbootstrap.com/icons/cart-fill/ -->
    <span>
      <svg xmlns="http://www.w3.org/2000/svg" width="16" height="16" fill="currentColor" class="bi bi-cart-fill"
        viewBox="0 0 16 16">
        <path
          d="M0 1.5A.5.5 0 0 1 .5 1H2a.5.5 0 0 1 .485.379L2.89 3H14.5a.5.5 0 0 1 .491.592l-1.5 8A.5.5 0 0 1 13 12H4a.5.5 0 0 1-.491-.408L2.01 3.607 1.61 2H.5a.5.5 0 0 1-.5-.5zM5 12a2 2 0 1 0 0 4 2 2 0 0 0 0-4zm7 0a2 2 0 1 0 0 4 2 2 0 0 0 0-4zm-7 1a1 1 0 1 1 0 2 1 1 0 0 1 0-2zm7 0a1 1 0 1 1 0 2 1 1 0 0 1 0-2z" />
      </svg>{{ count }}
    </span>
  </div>

  <img :src="product.image" class="w-50">

  <h3>{{ product.title }}</h3>

  <!-- v-html because description contains an <em> tag that should render, not be shown as text -->
  <div v-html="product.description"></div>

  <p>{{ calculated_price }}</p>

  <button class="btn btn-primary" :disabled="cartFull" @click="addToCart">Add to Cart</button>
  <!-- END OF ADDING OR MODIFYING YOUR CODE HERE -->
</template>

<style scoped>
/* Optional styling can go here */
</style>
