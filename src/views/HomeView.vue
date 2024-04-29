<script setup>
import { onMounted } from 'vue'; // Import onMounted from Vue
import NieuwsList from '@/components/nieuws/NieuwsList.vue';
import Trainingstijden from '@/components/trainingstijden/Trainingstijden.vue';

onMounted(() => {
 localStorage.setItem('token', 'ded');
});

</script>

<template>
 <div class="container-fluid">
    <div class="row">
      <div class="col-5">
        <h2>Nieuws</h2>
        <NieuwsList></NieuwsList>
      </div>
      <div class="col-5">
        <h2>Trainingstijden</h2>
        <Trainingstijden></Trainingstijden>
      </div>
    </div>
 </div>
</template>
