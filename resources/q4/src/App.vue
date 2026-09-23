<script setup>
import { ref, onMounted } from 'vue';

const numCoins = ref(1);
const isHeadList = ref([]); // Array storing whether each coin is heads (true) or tails (false)
const count = ref(0);

// ADD YOUR CODE HERE
const head = ref("img/head.png")
const tail = ref("img/tail.png")

function resizeCoins(){
    while (isHeadList.value.length!= numCoins.value){
    if (isHeadList.value.length<numCoins.value){
        isHeadList.value.push(head.value)
    }
    else{
        isHeadList.value.pop()
    }
}}

onMounted (()=>{
    isHeadList.value.push(tail.value)
})

function flip(){
    count.value+=isHeadList.value.length
    isHeadList.value =[]
    let numbergen = 0
    for (let i=0;i<numCoins.value;i++){
        numbergen = Math.round(Math.random())
        if (numbergen ===0){
            isHeadList.value.push(head.value)
        }
        else{
            isHeadList.value.push(tail.value)
        }
    }
}


// END OF ADDING YOUR CODE HERE
</script>

<template>
    <!-- ADD YOUR CODE HERE -->
     <div class="container-fluid">
<label class="mx-1">Number of coins</label>
<input class="w-50 mx-1" v-model="numCoins" @change ="resizeCoins">
<button class="btn btn-primary " @click="flip">flip</button>
</div>
<br>
<div>
    <img v-for="(coin,index) in isHeadList" :key="index" :src="coin" class="my-2">
</div>
<br>
<p>Flipped {{ count }} times</p>




    

    

    <!-- END OF ADDING YOUR CODE HERE -->
</template>

<style scoped>
/* Optional styling can go here */
</style>
