<script setup>
import { ref, onMounted } from 'vue';
import axios from 'axios';

const spelers = ref([]);
const team1 = ref('');
const team2 = ref('');
const schijdsrechter1 = ref('');
const schijdsrechter2 = ref('');
const tafel1 = ref('');
const tafel2 = ref('');
const datum = ref('');

onMounted(() => {
    axios.get('http://localhost/spelers')
        .then(response => {
            spelers.value = response.data;
        })
        .catch(error => console.error(error));
});

const createSpeler = () => {
    const wedstrijdData = {
        team1: team1.value, 
        team2: team2.value, 
        schijdsrechter1: schijdsrechter1.value,
        schijdsrechter2: schijdsrechter2.value,
        tafel1: tafel1.value,
        tafel2: tafel2.value,
        datum: datum.value
    };

    axios.post('http://localhost/wedstrijdschema', wedstrijdData)
        .then(response => {
            console.log('Wedstrijd created successfully', response);
            location.reload();  
        })
        .catch(error => console.error('Error creating wedstrijd', error));
};
</script>


<template>
    <div class="container-fluid">
        <div class="d-flex justify-content-between align-items-center">
            <h1>Wedstrijd maken</h1>
        </div>

        <div class="container mx-auto p-3">
            <form class="row g-3 border" @submit.prevent="submitForm">
                <div class="col-md-6">
                    <label for="team1" class="form-label">Thuis Team</label>
                    <input type="text" id="team1" class="form-control" v-model="team1"> 
                </div>
                <div class="col-md-6">
                    <label for="team2" class="form-label">Uit Team</label>
                    <input type="text" id="team2" class="form-control" v-model="team2"> 
                </div>
                <div class="col-md-6">
                    <label for="schijdsrechter1" class="form-label">Schijdsrechter 1</label>
                    <select id="schijdsrechter1" class="form-select" v-model="schijdsrechter1">
                        <option value="">Selecteer een schijdsrechter</option>
                        <option v-for="speler in spelers" :key="speler.id" :value="speler.id">[{{ speler.team }}] {{ speler.voornaam }} {{ speler.achternaam }}</option>
                    </select>
                </div>

                <div class="col-md-6">
                    <label for="schijdsrechter2" class="form-label">Schijdsrechter 2</label>
                    <select id="schijdsrechter2" class="form-select" v-model="schijdsrechter2">
                        <option value="">Selecteer een schijdsrechter</option>
                        <option v-for="speler in spelers" :key="speler.id" :value="speler.id">[{{ speler.team }}] {{ speler.voornaam }} {{ speler.achternaam }}</option>
                    </select>
                </div>

                <div class="col-md-6">
                    <label for="tafel1" class="form-label">Tafel 1</label>
                    <select id="tafel1" class="form-select" v-model="tafel1">
                        <option value="">Selecteer een tafel</option>
                        <option v-for="speler in spelers" :key="speler.id" :value="speler.id">[{{ speler.team }}] {{ speler.voornaam }} {{ speler.achternaam }}</option>
                    </select>
                </div>

                <div class="col-md-6">
                    <label for="tafel2" class="form-label">Tafel 2</label>
                    <select id="tafel2" class="form-select" v-model="tafel2">
                        <option value="">Selecteer een tafel</option>
                        <option v-for="speler in spelers" :key="speler.id" :value="speler.id">[{{ speler.team }}] {{ speler.voornaam }} {{ speler.achternaam }}</option>
                    </select>
                </div>

                <div class="col-md-6">
                    <label for="datum" class="form-label">Datum</label>
                    <input type="date" class="form-control" id="datum" v-model="datum">
                </div>
            </form>
            <button style="width: 100%" @click.prevent="createSpeler" class="btn btn-primary">Submit</button>
        </div>
    </div>
</template>

    