<script setup>
import { ref, onMounted } from 'vue';
import axios from 'axios';
import SpelerItem from './SpelerItem.vue';
import CreateSpeler from './CreateSpeler.vue';

const spelerItems = ref([]);
const createSpelerCheck = ref(false); 

onMounted(() => {
    axios.get('http://localhost/spelers')
        .then(results => {
            spelerItems.value = results.data;
            console.log(results); 
        })
        .catch(error => console.log(error));
});

function toggleCreateSpeler() { 
    createSpelerCheck.value = !createSpelerCheck.value; 
};

</script>


<template>
    <div v-if="createSpelerCheck">
        <CreateSpeler></CreateSpeler>
        <br></br>
        <button @click="toggleCreateSpeler"  style="width: 100%" class="btn btn-primary">Back</button>
    </div>
    <div  v-if="!createSpelerCheck">
        <h2>Spelers</h2>
        <button @click="toggleCreateSpeler" class="btn btn-primary">Create player</button>

        <div class="container-fluid">
            <div class="row">
                <div class="col-md-3 mb-4" v-for="(spelerItem, index) in spelerItems" :key="spelerItem.id">
                    <SpelerItem :spelerItem="spelerItem" />
                </div>
            </div>
        </div>
    </div>
</template>
    
