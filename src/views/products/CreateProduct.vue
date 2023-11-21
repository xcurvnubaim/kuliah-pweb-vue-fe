<script setup>
import { ref } from 'vue'
import axios from 'axios'

const data = ref(null);

const getData = async() => {
    try{
        const response = await axios.get(import.meta.env.VITE_API_URL + '/api/products', {withCredentials: true});
        data.value = response.data;
    } catch (e) {
        console.log(e);
    }
}


getData();

</script>
<template>
    {{data}}
</template>