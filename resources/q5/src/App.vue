<script setup>
import { ref, computed, onMounted } from 'vue';
import axios from 'axios';

const timestamp = ref(null);
const message = ref("");
const temperatureList = ref([]);
const average = ref(0)

// ADD YOUR CODE HERE
async function refresh(){
  average.value = 0
  temperatureList.value = []
  const response= await axios.get("https://api-open.data.gov.sg/v2/real-time/api/air-temperature")
  console.log(response)

  // Bug 1 fix: correct path — response.data.data (double nesting) and readings[0] (it's an array)
  const newTimestamp = response.data.data.readings[0].timestamp
  const temp_list = response.data.data.readings[0].data

  // TODO: pull response.data.data.stations into a stationList so you can look up
  // each reading's station name with .find(), then push { station: name, temperature: tempval.value }
  // instead of just the raw number below.
  const station_list = response.data.data.stations

  // Bug 2 fix: assign into the timestamp ref (.value) instead of shadowing it with a new local const
  timestamp.value = newTimestamp

  for (let i=0;i < temp_list.length;i++){
    const station = station_list[i].name
    const temp = temp_list[i].value
    const stationid = station_list[i].id
    const tempid = temp_list[i].stationId 
    if (stationid===tempid){
      temperatureList.value.push({station:station,temperature:temp})
      average.value+=temp
    } 

  }

  // Turn the running total into an actual average
  average.value = average.value / temp_list.length
  return 
}
onMounted (()=>{
  refresh()
})





// END OF ADDING YOUR CODE HERE
</script>

<template>
  <h1>
    Singapore temperature
  </h1>
  <h2>
    Average: {{ average.toFixed(2)}}
  </h2>
  <h2>
    {{ timestamp }}
  </h2>
  <button class="btn btn-primary btn-fluid" @click="refresh">refresh</button>
  <!-- ADD YOUR CODE HERE -->

  <table class="table table-bordered bordered-primary">
  <thead>
    <tr class="border">
      <th>Station</th>
      <th>Temperature</th>
    </tr>
  </thead>
  <tbody>
    <tr v-for="temperature in temperatureList" :key="temperature">
      <td>{{ temperature.station }}</td>
      <td>{{ temperature.temperature }}</td>
    </tr>
  </tbody>
</table>










  <!-- END OF ADDING YOUR CODE HERE -->
</template>

<style scoped>
/* Optional styling can go here */
</style>
