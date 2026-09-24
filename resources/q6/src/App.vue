<script setup>
import { ref } from 'vue';

const expression = ref('');//thisu will be the thing that is changing
const answer = ref('');//this is the output
const buttons = [
  1, 2, 3, '/',
  4, 5, 6, 'x',
  7, 8, 9, '-',
  0, '.', '=', '+',
  'AC', 'BK'
];
// ADD YOUR CODE HERE
function addinto(input){
  if (input !== "=" && input !== "AC" && input !== "BK"){
  expression.value+=input}
  else if(input === "AC"){
    expression.value= ""
  }
  else if(input ==="BK"){
    const expresslist = expression.value.split('')
    expresslist.pop()
    expression.value = expresslist.join('')}
  else{
    calculate(expression.value)
  }
  }

  const expressions = ["+","-","x","/"]//how do i priortise the expressions





// END OF ADDING YOUR CODE HERE
</script>

<template>
  <div class="container-fluid justify-content-center"> 
  <div class="border m-3 p-3 text-end" style="height: 100px;">
    <p>{{ expression }}</p>
    <p>{{ answer }}</p>
  </div>
  <div class="row row-cols-6 g-2 text-center">
<button class="btn btn-secondary mx-3 my-2" v-for="btn in buttons" :key="btn" @click="addinto(btn)">{{ btn }}</button>
</div>
</div>
  <!-- ADD YOUR CODE HERE -->








  

  <!-- END OF ADDING YOUR CODE HERE -->
</template>

<style scoped>
/* Optional styling can go here */
</style>
