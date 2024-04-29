<script setup>
import { ref } from 'vue';
import axios from 'axios';

const voornaam = ref('');
const achternaam = ref('');
const geboortedatum = ref('');
const team = ref('');
const fieldsEmpty = ref(false);

function createSpeler() {
    if(voornaam.value == '' || achternaam.value == '' || geboortedatum.value == '' || team.value == ''){
        fieldsEmpty.value = true;
    }
    else{
        fieldsEmpty.value = false;
        
        axios.post('http://localhost/spelers', {
            voornaam: voornaam.value,
            achternaam: achternaam.value,
            geboortedatum: geboortedatum.value,
            team: team.value
        })
        .then(response => {
            console.log(response);
            location.reload();
        })
        .catch(error => {
            console.error(error);
        });
    }
}
</script>

<template>
<div class="container-fluid">
    <h1>Speler maken</h1>
    <form class="row g-3"> 
        <div class="form-group">
            <label for="voornaam">Voornaam</label>
            <input type="text" class="form-control" id="voornaam" name="voornaam" v-model="voornaam" placeholder="Voornaam">
        </div>
        <div class="form-group">
            <label for="achternaam">Achternaam</label>
            <input type="text" class="form-control" name="achternaam" id="achternaam" v-model="achternaam" placeholder="Achternaam">
        </div>
        <div class="form-group">
            <label for="geboortedatum">Geboortedatum</label>
            <input type="date" class="form-control" name="geboortedatum" id="geboortedatum" v-model="geboortedatum">
        </div>
        <div class="form-group">
            <label for="team">Team</label>
            <input type="text" class="form-control" id="team" name="team" v-model="team" placeholder="Team">
        </div>
        <p v-if="fieldsEmpty" id="notFilledIn">Not all fields are filled in</p>
        <button @click.prevent="createSpeler" class="btn btn-primary">Submit</button>
    </form>
</div>
</template>

<style scoped>
#notFilledIn {
    color: red;
}
</style>
