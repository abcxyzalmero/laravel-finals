<script lang="ts">
import axios from 'axios';
import { ref } from 'vue';

export default {
    setup() {
        const name = ref('');
        const email = ref('');
        const password = ref('');

        async function register() {
            try {
                await axios.post('http://127.0.0.1:8000/register', {
                    name: name.value,
                    email: email.value,
                    password: password.value
                });
                alert('Registration successful');
            } catch {
                alert('Registration failed');
            }
        }

        return {
            name,
            email,
            password,
            register
        };
    }
};
</script>

<template>
    <main>
        <form @submit.prevent="register" class="register-page">
            <div class="register-box">
                <h1>Register</h1>
                <input type="text" v-model="name" placeholder="Name" required>
                <input type="email" v-model="email" placeholder="Email" required>
                <input type="password" v-model="password" placeholder="Password" required>
                <button type="submit">Register</button>
            </div>
        </form>
    </main>
</template>

<style>
.register-page {
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
    height: 100vh;
}

.register-box {
    display: flex;
    flex-direction: column;
    gap: 1rem;
    padding: 1rem;
    border: 1px solid #ccc;
    border-radius: 5px;
    background-color: #afafaf;
}

.register-box input {
    padding: 0.5rem;
    border: 1px solid #ccc;
    border-radius: 5px;
}

.register-box button {
    padding: 0.5rem;
    border: none;
    border-radius: 5px;
    background-color: #333;
    color: #fff;
}

.register-box h1 {
    margin: 0;
    text-align: center;
    font-size: 1.5rem;
    color: #d6d6d6;
}
</style>