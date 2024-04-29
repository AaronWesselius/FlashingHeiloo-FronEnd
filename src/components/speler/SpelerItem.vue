<script setup>
import { defineProps, ref } from 'vue';
import axios from 'axios';

const props = defineProps({
    spelerItem: Object,
});

const id = ref(props.spelerItem.id);
const voornaam = ref(props.spelerItem.voornaam);
const achternaam = ref(props.spelerItem.achternaam);
const geboortedatum = ref(props.spelerItem.geboortedatum);
const team = ref(props.spelerItem.team);

const edit = ref(false); 

const toggleEdit = () => {
    edit.value = !edit.value;
    if(!edit.value){
        axios.put(`http://localhost/spelers/${id.value}`, {
            id: id.value,
            voornaam: voornaam.value,
            achternaam: achternaam.value,
            geboortedatum: geboortedatum.value,
            team: team.value
        })
        .then(response => {
            console.log(response);
        })
        .catch(error => {
            console.error(error);
        });
    }
};

const deleteSpelerItem = () => {
    axios.delete(`http://localhost/spelers/${id.value}`)
        .then(response => {
            console.log(response);
            location.reload();
        })
        .catch(error => {
            console.log(error);
    });
};
</script>


<template>
    <div v-if="!edit" class="card border-success custom-card-width"> 
        <div class="card-body">
            <h2 class="card-title">{{ voornaam }} {{ achternaam }}</h2>
            <p class="card-text">{{ team }}</p>
            <p class="card-text">{{ geboortedatum }}</p>
            <button style="width: 100%" type="submit" class="btn btn-warning btn-block" @click="toggleEdit" >Update</button> 
            <button style="width: 100%" type="submit" class="btn btn-danger btn-block" @click="deleteSpelerItem">Delete</button> 
        </div>
    </div>
    <div v-if="edit" class="card border-success custom-card-width">
        <div class="card-body">
            <input type="text" id="voornaam" name="voornaam" v-model="voornaam" placeholder="voornaam">
            <input type="text" id="achternaam" name="achternaam" v-model="achternaam" placeholder="achternaam">
            <input type="text" id="team" name="team" v-model="team" placeholder="team">
            <input type="date" id="geboortedatum" name="geboortedatum" v-model="geboortedatum" placeholder="geboortedatum">
            <button style="width: 100%" type="submit" class="btn btn-warning btn-block" @click="toggleEdit" >Confirm</button> 
            <button style="width: 100%" type="submit" class="btn btn-danger btn-block" @click="deleteSpelerItem">Delete</button> 
        </div>
    </div>
</template>
    

  
<style scoped>

</style>