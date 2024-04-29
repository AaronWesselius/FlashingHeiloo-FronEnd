<script setup>
import { ref, onMounted } from 'vue';
import LogIn from '@/components/admin/Login.vue';
import LogedIn from '@/components/admin/AdminLoggedIn.vue';

const token = ref(null);

onMounted(() => {
 token.value = localStorage.getItem('token');
});

</script>

<template>
    <LogIn v-if="token !== 'rwqdgrxgbw'"></LogIn>
    <LogedIn v-else></LogedIn>
</template>
