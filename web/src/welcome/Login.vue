<script setup lang="ts">
import { ref } from 'vue';
import { useRouter } from 'vue-router';
import { RouteNames } from '../router';
import { useAuth } from '../common/auth';

import TokenIcon from '../assets/shot-token.jpg';

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
        <div class="signup-info">
            <div>
                <p>New User?</p>
                <router-link :to="{ name: RouteNames.Signup }">
                    <button class="primary">Signup</button>
                </router-link>
                <p>And get <img :src="TokenIcon" /> Tokens</p>

            </div>
        </div>
        <div class="login-form">
            <div>
                <!-- <label for="username">Email</label> -->
                <input type="text" name="username" v-model="username" placeholder="Username" />
                <!-- <label for="password">Password</label> -->
                <input type="password" name="password" v-model="password" placeholder="Password" />
                <button class="secondary" @click="beginLogin()">Login</button>
            </div>
        </div>
    </div>
</template>

<style lang='scss' scoped>
button {
    width: 200px;
}
.signup-info {
    color: #762dc4;
    border-bottom: 1px solid #d4d2fb;
    padding-bottom: 40px;
    margin: 40px;
    display: flex;
    justify-content: center;
    > div {
        display: flex;
        flex-direction: column;
        max-width: 200px;

        button {
            margin-top: 20px;
            margin-bottom: 20px;
        }
        img {
            margin-bottom: -8px;
            height: 30px;
            width: 30px;
        }
    }
}
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

        ::placeholder {
            color: #b5b2fb;
            opacity: 1;
        }

        input {
            margin-bottom: 20px;
        }
    }
}
</style>
