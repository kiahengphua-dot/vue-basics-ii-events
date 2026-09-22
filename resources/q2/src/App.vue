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
let output = ""
const my_price = product.value.price
if (my_price>0){
  const string_price = my_price.toString()
  const cents= string_price.slice(-2)
  const dollars = string_price.slice(0,-2)
  const format_dollar = Number(dollars).toLocaleString()
   output = "$"+format_dollar+"."+ cents
}
else{
   output = "$"+"0"
}


// END OF ADDING YOUR CODE HERE
</script>

<template>
  <!-- ADD OR MODIFY YOUR CODE HERE -->

  <!-- Shopping cart icon; https://icons.getbootstrap.com/icons/cart-fill/ -->
  <div class="row">
  <div class="col-6">
<div class="fs-2 mx-2">{{ sitename }}</div>
<img :src="product.image" class="img-fluid">
  </div>
  <div class="col-6">
  <svg xmlns="http://www.w3.org/2000/svg" width="16" height="16" fill="currentColor" class="bi bi-cart-fill"
    viewBox="0 0 16 16">
    <path
      d="M0 1.5A.5.5 0 0 1 .5 1H2a.5.5 0 0 1 .485.379L2.89 3H14.5a.5.5 0 0 1 .491.592l-1.5 8A.5.5 0 0 1 13 12H4a.5.5 0 0 1-.491-.408L2.01 3.607 1.61 2H.5a.5.5 0 0 1-.5-.5zM5 12a2 2 0 1 0 0 4 2 2 0 0 0 0-4zm7 0a2 2 0 1 0 0 4 2 2 0 0 0 0-4zm-7 1a1 1 0 1 1 0 2 1 1 0 0 1 0-2zm7 0a1 1 0 1 1 0 2 1 1 0 0 1 0-2z" />
  </svg>
  {{ count }}<br>
   <div class="fs-2">{{ product.title }}</div>
   <div v-html="product.description"></div>
   <div class="my-3"> {{ output }}</div>
   <button class="btn btn-primary" @click="count<10?count++:count" :disabled="count===10"">Add to Cart</button>
  </div>
  </div>








  <!-- END OF ADDING OR MODIFYING YOUR CODE HERE -->
</template>

<style scoped>
/* Optional styling can go here */
</style>
