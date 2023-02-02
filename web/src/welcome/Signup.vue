<script setup lang="ts">
import * as client from '@app/client';
import { ref } from 'vue';
import { useRouter } from 'vue-router';
import { RouteNames } from '../router';
import { useAuth } from '../common/auth';

const router = useRouter();

const { login } = useAuth();

const nickname = ref('');
const email = ref('');
const password = ref('');

async function beginSignup() {
    try {
        const config = new client.Configuration({ basePath: import.meta.env.VITE_SERVICE_HOST })
        const response = await new client.AccountApi(config).accountControllerCreateAccount({
            createAccountRequest: {
                nickname: nickname.value,
                email: email.value,
                password: password.value,
            }
        });
        console.log(response)
        await login(email.value, password.value);
        router.replace({ name: RouteNames.Home })
    } catch (error) {
        console.log(error);
    }
}
</script>

<template>
    <div>
        <h2>Signup</h2>
        <div class="signup-form">
            <div>
                <input type="text" v-model="nickname" />
                <input type="text" v-model="email" />
                <input type="password" v-model="password" />
                <button @click="beginSignup()">Signup</button>
            </div>
        </div>
    </div>
</template>

<style lang='scss' scoped>
.signup-form {
    display: flex;
    justify-content: center;

    >div {
        display: flex;
        flex-direction: column;
        max-width: 200px;
    }
}
</style>
