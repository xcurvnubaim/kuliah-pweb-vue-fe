<script setup>
import { ref } from 'vue'
import axios from 'axios'
import { useRouter } from 'vue-router';
const data = ref(null);

const router = useRouter();
const getData = async() => {
    try{
        const response = await axios.get(import.meta.env.VITE_API_URL + '/api/products', {withCredentials: true});
        data.value = response.data;
    } catch (e) {
        router.push('/login');
    }
}


getData();

</script>
<template>
    {{data}}
</template>