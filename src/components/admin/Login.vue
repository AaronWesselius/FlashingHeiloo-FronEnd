<script setup>
import { ref } from 'vue';
import axios from 'axios';

const password = ref('');
const passwordIncorrect = ref(false); 

const login = async () => {
    try {
        const response = await axios.post('http://localhost/login', {
            wachtwoord: password.value
        }, {
            headers: {
                'Content-Type': 'application/json'
            }
        });

        if (response.status === 200) {
            localStorage.setItem('token', 'rwqdgrxgbw');
            location.reload();
        } else {
            passwordIncorrect.value = true; 
        }
    } catch (error) {
        passwordIncorrect.value = true; 
    }
};
</script>

<template>
    <div class="container vh-100 d-flex justify-content-center align-items-center mt-1">
        <form class="row g-3" method="POST">       
            <div class="mb-4">
                <label class="form-label">Wachtwoord</label>
                <input type="password" class="form-control" id="wachtwoord" name="wachtwoord" placeholder="wachtwoord" v-model="password">
                <label id="wrongPassword" class="form-label" v-if="passwordIncorrect">Wrong Password</label>
            </div>
            <button @click.prevent="login" class="btn btn-primary">Submit</button>           
        </form>
    </div>
</template>

<style scoped>
#wrongPassword {
    color: red;
}
</style>
