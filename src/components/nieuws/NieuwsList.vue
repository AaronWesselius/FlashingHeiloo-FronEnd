<script setup>
import { ref, onMounted } from 'vue';
import axios from 'axios';
import NieuwsItem from './NieuwsItem.vue';

const nieuwsItems = ref([]);

onMounted(() => {
    axios.get('http://localhost/nieuws')
        .then(results => {
            nieuwsItems.value = results.data;
            console.log(results); 
        })
        .catch(error => console.log(error));
});
</script>

<template>
   <div class="accordion" id="accordionExample">
        <div class="accordion-item" v-for="(nieuwsItem, index) in nieuwsItems" :key="nieuwsItem.id">
            <h2 class="accordion-header">
            <button class="accordion-button" type="button" :data-bs-toggle="'collapse'" :data-bs-target="`#collapse${index}`" :aria-expanded="index === 0" :aria-controls="`collapse${index}`">
                {{ nieuwsItem.kop }}
            </button>
            </h2>
            <div :id="`collapse${index}`" class="accordion-collapse collapse" :class="{'show': index === 0}" data-bs-parent="#accordionExample">
            <div class="accordion-body">
                <NieuwsItem :nieuwsItem="nieuwsItem" />
            </div>
            </div>
        </div>
    </div>

</template>
