<script setup>
import { ref, onMounted } from 'vue';
import axios from 'axios';
import WedstrijdItem from './WedstrijdItem.vue';
import CreateWedstrijd from './CreateWedstrijd.vue';

const createWedstrijd = ref(false);
const wedstrijdItems = ref([]);

function toggleCreateWedstrijd() {
    createWedstrijd.value = !createWedstrijd.value;
}
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
        <div v-if="!createWedstrijd">
            <h2>Wedstrijden</h2>
            <button @click="toggleCreateWedstrijd" class="btn btn-primary">Maken</button>
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
                        <th>Delete</th>
                    </tr>
                </thead>
                <tbody>
                    <WedstrijdItem v-for="wedstrijdItem in wedstrijdItems" :key="wedstrijdItem.id" :wedstrijdItem="wedstrijdItem" />
                </tbody>
            </table>    
        </div>
        <div v-if="createWedstrijd">
            <CreateWedstrijd></CreateWedstrijd>
            <br></br>
            <button @click="toggleCreateWedstrijd"  style="width: 100%" class="btn btn-primary">Back</button>
        </div>
    </div>
</template>
