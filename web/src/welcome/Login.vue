<script setup lang="ts">
import { ref } from 'vue';
import { useRouter } from 'vue-router';
import { RouteNames } from '../router';
import { useAuth } from '../common/auth';

const router = useRouter();

const { login } = useAuth();

const username = ref('');
const password = ref('');

async function beginLogin() {
    try {
        await login(username.value, password.value);
        router.replace({ name: RouteNames.Home })
    } catch (error) {
        console.log(error);
    }
}
</script>

<template>
    <div>
        <div class="login-form">
            <div>
                <label for="username">Email</label>
                <input type="text" name="username" v-model="username" />
                <label for="password">Password</label>
                <input type="password" name="password" v-model="password" />
                <button @click="beginLogin()">Login</button>
            </div>
        </div>
    </div>
</template>

<style lang='scss' scoped>
.login-form {
    display: flex;
    justify-content: center;
    text-align: left;

    >div {
        display: flex;
        flex-direction: column;
        max-width: 200px;
        label {
            margin-bottom: 5px;
            font-size: 14px;
        }

        input {
            margin-bottom: 20px;
        }
    }
}
</style>
