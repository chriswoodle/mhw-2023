<script setup lang="ts" >
import * as client from '@app/client';
import { defineComponent } from 'vue';
import { useRouter } from 'vue-router';

import { RouteNames } from '../router';
import { useAuth } from '../common/auth';
import HelloWorld from '../components/HelloWorld.vue';

import Plus from '../assets/plus.svg'
import Redeem from '../assets/redeem.svg'
import BalloonImage from '../assets/balloon.jpg'
import Place1Image from '../assets/place1.jpg'
import Place2Image from '../assets/place2.jpg'

import Person1Image from '../assets/person1.jpg'
import Person2Image from '../assets/person2.jpg'
import Person3Image from '../assets/person3.jpg'


const router = useRouter();
const { logout } = useAuth();

async function authLogout() {
    await logout();
    router.replace({ name: RouteNames.Login })
}


const posts = [
    {
        tokens: 75,
        image: BalloonImage,
        profile: Person1Image,
        title: 'Dream Balloon Rides',
        profileName: 'Noah Martin',
        favorited: 16,
        redeemed: 7
    },
    {
        tokens: 60,
        image: Place1Image,
        profile: Person2Image,
        title: 'Cozmo Coffee',
        profileName: 'Jack Millier',
        favorited: 6,
        redeemed: 8
    },
    {
        tokens: 100,
        image: Place2Image,
        profile: Person3Image,
        title: 'Bakeology',
        profileName: 'Amelia Garcia',
        favorited: 10,
        redeemed: 3
    }
]

</script>
<template>
    <div>
        <div class="post" v-for="post in posts">
            <div class="left">
                <div></div>
                <div class="image"><img :src="post.image" /></div>
            </div>
            <div class="right">
                <div class="poster">
                    <div><img :src="post.profile"/></div>
                    <div>{{ post.profileName }}</div>
                </div>
                <div class="title">
                    {{ post.title }}
                </div>
                <div class="action">
                    <div><img :src="Plus"/></div>
                    <div>
                        {{ post.favorited }} favorited

                    </div>
                </div>
                <div class="action">
                    <div>
                        <img :src="Redeem"/>
                    </div>
                    <div>
                        {{ post.redeemed }} redeemed
                    </div>

                </div>
            </div>
        </div>
    </div>
    <div>
        <button @click="authLogout()">Logout</button>
    </div>

</template>



<style lang='scss' scoped>
.post {
    // border: 1px solid red;
    box-shadow: 0 1px 3px rgba(0, 0, 0, 0.12), 0 1px 2px rgba(0, 0, 0, 0.24);
    border-radius: 10px;
    padding: 10px;
    display: flex;

    .left {

        .image {
            img {
                height: 120px;
                width: 120px;
                border-radius: 10px;
            }
        }
    }

    .right {
        margin-left: 20px;
        display: flex;
        flex-direction: column;

        >div {
            display: flex;
        }
        .poster {
            font-size: 12px;
            color: #762ec3;
            font-weight: bold;
            margin-bottom: 5px;
            display: flex;
            align-items: center;
            img {
                height: 20px;
                border-radius: 5px;
                margin-right: 10px;
            }
        }
        .title {
            color: #762ec3;
            font-weight: bold;
            margin-bottom: 20px;
        }

        .action {
            color: #762ec3;
            display: flex;
            align-items: center;
            img {
                margin-right: 10px;
            }
        }
    }
}
</style>
