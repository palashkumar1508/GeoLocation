<template>
        <form action="" @submit.prevent="validation" >
            <div class="flex flex-col gap-8 justify-center p-14 items-center rounded-lg bg-[#000000] text-2xl text-[#0ACFE8]">
                <h1 class="text-7xl">Address</h1> 
                <div>
                    <label> Latitude : </label>
                    <input class="" type="text" placeholder="Enter Latitude"  v-model="lat">
                </div>
                <div>
                    <label>Longitude : </label>
                    <input type="text" v-model="lon"  placeholder="Enter Longitude">
                </div>
                <button @click="getLoc" class="p-5 text-red-500 shadow-md shadow-[#0ACFE8] rounded-lg">Find</button>
                <!-- <div v-if="!posts" class="text-white">{{ posts[0].display_name }}</div> -->
                <h1 v-if="res">{{ res }}</h1>

            </div>
        </form>

</template>

<script setup>
import {ref, onMounted}  from 'vue'
import axios from 'axios'
let lat = ref(null)
let lon = ref(null)
let res = ref('')


async function getLoc (){
    axios.get(`https://nominatim.openstreetmap.org/search.php?q=${lat.value}%2C+${lon.value}&format=jsonv2`).then((response)=>{
        res.value = response.data[0].display_name
    })

return;
}

</script>

<style scoped>

input{
    @apply p-3 rounded-md m-4
}

</style>
