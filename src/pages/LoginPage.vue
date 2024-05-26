<script lang="ts">
import axios from "axios";
import { ref } from 'vue'
import { useRouter } from 'vue-router'

export default {
    setup() {
        const email = ref('')
        const password = ref('')
        const router = useRouter()

        async function handleSubmit(event: Event) {
            event.preventDefault();
            try {
                await axios.post('http://127.0.0.1:8000/login', {
                    email: email.value,
                    password: password.value,
                });

                alert('Login successful');
                router.push('/dashboard/home');

            } catch (error) {
                console.error('Error:', error);
                alert('Invalid Credentials. Please try again.');
            }
        }

        return {
            email,
            password,
            handleSubmit
        }
    }
}
</script>

<template>
    <div>
        <form class="login-page">
            <div class="login-box">
                <h1>Login</h1>
                <input type="email" v-model="email" placeholder="Email" required>
                <input type="password" v-model="password" placeholder="Password" required>
                <button @click="handleSubmit">Login</button>
            </div>
        </form>
    </div>
</template>

<style>
.login-page {
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
    height: 100vh;
}

.login-box {
    display: flex;
    flex-direction: column;
    gap: 1rem;
    padding: 1rem;
    border: 1px solid #ccc;
    border-radius: 5px;
    background-color: #afafaf;
}

.login-box input {
    padding: 0.5rem;
    border: 1px solid #ccc;
    border-radius: 5px;
}

.login-box button {
    padding: 0.5rem;
    border: none;
    border-radius: 5px;
    background-color: #333;
    color: #fff;
}

.login-box h1 {
    margin: 0;
    text-align: center;
    font-size: 1.5rem;
    color: #d6d6d6;
}
</style>
