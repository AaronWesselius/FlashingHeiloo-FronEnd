<script setup>
import { ref, onMounted } from 'vue';
import axios from 'axios';
import WedstrijdItem from './WedstrijdItemXKnop.vue';


const wedstrijdItems = ref([]);

onMounted(() => {
    axios.get('http://localhost/wedstrijdschema')
        .then(results => {
            wedstrijdItems.value = results.data;
            console.log(results); 
        })
        .catch(error => console.log(error));
});
</script>

<template>
    <div class="container-fluid">
            <h2>Wedstrijden</h2>
            <table class="table" id="programma-table">
                <thead>
                    <tr>
                        <th>Thuis team</th>
                        <th>Uit team</th>
                        <th>schijdsrechter1</th>
                        <th>schijdsrechter2</th>
                        <th>tafel1</th>
                        <th>tafel2</th>
                        <th>Datum</th>
                    </tr>
                </thead>
                <tbody>
                    <WedstrijdItem v-for="wedstrijdItem in wedstrijdItems" :key="wedstrijdItem.id" :wedstrijdItem="wedstrijdItem" />
                </tbody>
            </table>    
        </div>
</template>
