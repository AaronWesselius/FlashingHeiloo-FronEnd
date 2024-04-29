<script setup>
import { defineProps, ref, onMounted } from 'vue';
import axios from 'axios';

const props = defineProps({
    wedstrijdItem: Object,
});

const { id, team1, team2, schijdsrechter1, schijdsrechter2, tafel1, tafel2, datum } = props.wedstrijdItem;

const theschijdsrechter1 = ref('');
const theschijdsrechter2 = ref('');
const thetafel1 = ref('');
const thetafel2 = ref('');

onMounted(async () => {
    theschijdsrechter1.value = await getSpelers(schijdsrechter1);
    theschijdsrechter2.value = await getSpelers(schijdsrechter2);
    thetafel1.value = await getSpelers(tafel1);
    thetafel2.value = await getSpelers(tafel2);
});

async function getSpelers($speler) {
    try {
        const response = await axios.get(`http://localhost/spelers/${$speler}`);
        return response.data;
    } catch (error) {
        console.error(error);
        return null;
    }
}

</script>

<template>
    <tr class="wedstrijd-item">
        <td>{{ team1 }}</td>
        <td>{{ team2 }}</td>
        <td>{{ theschijdsrechter1.voornaam }}</td>
        <td>{{ theschijdsrechter2.voornaam }}</td>
        <td>{{ thetafel1.voornaam }}</td>
        <td>{{ thetafel2.voornaam }}</td>
        <td>{{ datum }}</td>
    </tr>
</template>

<style scoped>

</style>
