<script setup>
import { ref, computed } from 'vue';

const animals = ref(["🐖", "🐓", "🐄", "🐑"]);
const animal = ref(undefined);
const farm = ref([]);

// Computed property that returns two different random animals each time it's accessed
const today_animals = computed(() => {
  const arr = [];
  // ADD YOUR CODE HERE
 while (arr.length <2){
    let randomised = Math.floor(Math.random()*animals.value.length)
    if (!arr.includes(animals.value[randomised])){
    arr.push(animals.value[randomised])}
  }
  // END OF ADDING YOUR CODE HERE
  return arr;
});
// ADD YOUR CODE HERE

function add_animal() {
  if (animal.value != undefined){
  farm.value.push(animal.value)}
}





// END OF ADDING YOUR CODE HERE
</script>

<template>
  <h2>Today's animals</h2>
  <!-- ADD YOUR CODE HERE -->
   <br>
   <div v-for="item in today_animals">
    <input type="radio" :value ="item" v-model="animal">{{ item }}
   </div>
   <br><br>
   <button @click ="add_animal" class="btn btn-success">Add to farm</button>
   <br>
<div v-if="farm.length>0"><p>Your farm consists of {{ farm.join() }}</p></div>






  <!-- END OF ADDING YOUR CODE HERE -->
</template>

<style scoped>
/* Optional styling can go here */
</style>
