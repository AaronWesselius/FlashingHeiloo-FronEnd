<template>
    <div id="data-container">
       <table class="table" id="programma-table">
         <thead>
           <tr>
             <th v-for="header in headers" :key="header">{{ header }}</th>
           </tr>
         </thead>
         <tbody>
           <tr v-for="item in data" :key="item.id">
             <td v-for="header in headers" :key="header">{{ item[header] }}</td>
           </tr>
         </tbody>
       </table>
    </div>
   </template>
   
   <script>
   import { ref, onMounted } from 'vue';
   import axios from 'axios';
   
   export default {
    setup() {
       const data = ref([]);
       const headers = ref([]);
   
       onMounted(async () => {
         try {
           const response = await axios.get('http://localhost/trainingstijden');
           data.value = response.data;
           headers.value = Object.keys(response.data[0]);
         } catch (error) {
           console.error(error);
         }
       });
   
       return { data, headers };
    },
   };
   </script>
   