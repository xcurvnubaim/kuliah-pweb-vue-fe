<script setup>
import { ref } from 'vue'
import axios from 'axios'
import editIcon from '../../assets/pencil-solid.svg'
import deleteIcon from '../../assets/trash-solid.svg'

const data = ref(null);
const myId = ref(null);

const getMe = async () => {
    try {
        const response = await axios.get(import.meta.env.VITE_API_URL + '/api/users/me', { withCredentials: true });
        console.log(response.data);
        myId.value = response.data.user.id;
        getData();
    }catch (e) {
        console.log(e);
    }
}

const getData = async () => {
    try {
        console.log(myId.value)
        const response = await axios.get(import.meta.env.VITE_API_URL + '/api/products?where[tenant_id][equals]=' + myId.value , { withCredentials: true });
        data.value = response.data;
    } catch (e) {
        console.log(e);
    }
}

getMe()

</script>
<template>
    <div class="w-screen">
        <div class="flex justify-center">
            <h1 class="text-4xl font-bold text-red-500">Products</h1>
        </div>
        <div class="flex justify-center">
            <table class="mx-5">
                <thead>
                    <tr>
                        <th class="border border-slate-800 px-5">No</th>
                        <th class="border border-slate-800 px-5">Item Name</th>
                        <th colspan="2" class="border border-slate-800 px-5">Price</th>
                        <th colspan="2" class="border border-slate-800 px-5">Action</th>
                    </tr>
                </thead>
                <tbody>
                    <tr v-if="data" v-for="(item, index) in data.docs">
                        <td class="border border-slate-800 px-5">{{ index+1 }}</td>
                        <td class="border border-slate-800 px-5">{{ item.name }}</td>
                        <td class="border border-b-slate-800 border-r-transparent">Rp</td>
                        <td class="border border-slate-800 pl-5 text-right">{{ new Intl.NumberFormat('id-ID').format(item.price) }}</td>
                        <td class="px-3 py-1 border border-slate-800 hover:bg-blue-300 cursor-pointer"><img :src="editIcon" alt="" height="2px"></td>
                        <td class="px-3 py-1 border border-slate-800 hover:bg-red-300 cursor-pointer"><img :src="deleteIcon" ></td>
                    </tr>
                </tbody>
            </table>
        </div>
    </div>
</template>