<script setup>
import { defineProps } from 'vue';

const props = defineProps({
    nieuwsItem: Object,
});

const { id, kop, date, text } = props.nieuwsItem;
</script>

<template>
    <div class="nieuws-item">
        <b class="date">{{ date }}</b>
        <p>{{ text }}</p>
    </div>
</template>
 
  
<style scoped>

</style>