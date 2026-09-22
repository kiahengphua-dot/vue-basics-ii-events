<script setup>
import { ref, computed } from 'vue';

const sentence = ref("We love Bootstrap! We love Vue.js! ");
const colors = ref(["red", "orange", "green"]);

// ADD YOUR CODE HERE
//make it so that each index has a corrospondoing to colors 
//attach that color to each of the letter so like we color:red love color blue 
const styled_words = computed(()=>{
  const sentence_array = sentence.value.split(" ")
  const colored_array = []
  for (let i=0;i<sentence_array.length;i++){
    let color_index = i%3
    if (i%2===1){
      colored_array.push({color: colors.value[color_index], word: sentence_array[i],underline:true})
  }
  else{
    colored_array.push({color: colors.value[color_index], word: sentence_array[i],underline:false})
  }
  
}
return colored_array
})


// END OF ADDING YOUR CODE HERE
</script>

<template>
  <!-- ADD YOUR CODE HERE -->

<p>Sentence<input type="text" v-model="sentence" class="w-50"></p>
<span v-for="word in styled_words" :key="word.word" :style="{ color: word.color, textDecoration: word.underline ? 'underline' : 'none'}" class="me-2">{{ word.word }}  </span>










  <!-- END OF ADDING YOUR CODE HERE -->
</template>

<style scoped>
/* Optional styling can go here */
</style>
