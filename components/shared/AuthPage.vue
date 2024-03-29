<script setup lang="ts">
</script>

<script>
import axios from 'axios';
import { library } from '@fortawesome/fontawesome-svg-core'
import { FontAwesomeIcon } from '@fortawesome/vue-fontawesome'
import { faEnvelope, faLock } from '@fortawesome/free-solid-svg-icons'
import { createStore } from 'vuex'
import { mapActions } from 'vuex'

export default {
    props: {
        isRegister: {
            type: Boolean,
            default: false
        }
    },
    components: {
        FontAwesomeIcon
    },

    data() {
        return {
            email: '',
            password: '',
            username: '',
        };
    },
    mounted() {
        library.add(faEnvelope, faLock)
    },
    methods: {
        async handleSubmit() {
            if (!this.isRegister) {
                const response = await axios.post('http://localhost:1337/auth/local', {
                    identifier: this.email,
                    password: this.password,
                }, {
                    headers: {
                        'content-Type': 'application/json',
                    },
                })
                if (response.data.jwt) {
                    const userDetails = await axios.get('http://localhost:1337/users/me', {
                        headers: {
                            Authorization:
                                'Bearer ' + response.data.jwt,
                        },
                    })
                    localStorage.setItem('jwt', response.data.jwt)
                    localStorage.setItem('user', JSON.stringify(userDetails.data))
                    this.$router.push('/map');
                } else {
                    console.log(response.data.message);
                }
            } else {
                await axios.post('http://localhost:1337/auth/local/register', {
                    username: this.username,
                    email: this.email,
                    password: this.password,
                })
                    .then(response => {
                        localStorage.setItem('user', JSON.stringify(response.data.user));
                        localStorage.setItem('jwt', response.data.jwt);
                        this.$router.push('/map');
                    })
                    .catch(error => {
                        console.log('An error occurred:', error.response);
                    });
            }
        },
    },
};
</script>

<template>
    <div class="flex h-screen">
        <div class="flex pt-8 ml-6 justify-between absolute w-[100%]">
            <h2 class="text-[24px] font-bold font-integral text-black"><a href="./">INFLINE</a></h2>
            <h2 class="text-[15px] text-white mr-24">+94 0116 789 754</h2>
        </div>
        <div class="w-1/2 flex items-center justify-center mt-12">
            <div class="p-8 ml-[-80px]">
                <h2 class="text-[30px] font-bold mb-8 font-integral">{{ isRegister ? 'S\'INSCRIRE' : 'SE CONNECTER' }}</h2>
                <p v-if="!isRegister" class="mb-4">Si tu n’es pas encore inscrit,<br> Tu peux <span
                        class="text-purpleMDS"><a href="./register"> t’inscrire ici !</a></span></p>
                <p v-else class="mb-4">Tu es déjà inscrit ? <br>Tu peux <span class="text-purpleMDS"><a href="./login">te
                            connecter ici</a></span>
                </p>
                <form class="mt-12" v-on:submit.prevent="handleSubmit">
                    <div class="mb-4 relative">
                        <label class="block text-greyTextMDS text-[13px]" for="email">
                            Email
                        </label>
                        <input class="bg-transparent w-[350px] py-2 px-3 border-b-black border-transparent" id="email"
                            type="text" placeholder="Entre ton adresse e-mail" v-model="email" />
                        <!--<font-awesome-icon icon="fa-solid fa-envelope" class="absolute top-8 left-[-14px]"/>-->
                    </div>
                    <div v-if="isRegister" class="mb-4">
                        <label class="block text-greyTextMDS text-[13px]" for="username">
                            Nom d'utilisateur
                        </label>
                        <input class="w-full py-2 px-3 border-b-black border-transparent" id="username"
                            type="text" placeholder="Entre ton nom d'utilisateur" v-model="username"/>
                    </div>
                    <div class="mb-4">
                        <label class="block text-greyTextMDS text-[13px]" for="password">
                            Mot de passe
                        </label>
                        <input class=" w-full py-2 px-3 border-b-black border-transparent" id="password" type="password"
                            placeholder="Entre ton mot de passe" v-model="password" />
                        <!--<font-awesome-icon icon="fa-solid fa-lock" class="absolute top-8 left-[-14px]"/>-->
                    </div>
                    <div v-if="isRegister" class="mb-4">
                        <label class="block text-greyTextMDS text-[13px]" for="confirmPassword">
                            Confirmer le mot de passe
                        </label>
                        <input class="w-full py-2 px-3 border-b-black border-transparent" id="confirmPassword"
                            type="password" placeholder="Confirme ton mot de passe" />
                    </div>
                    <div class="flex items-center justify-between mt-8">
                        <button class="bg-purpleMDS text-white font-bold py-3 px-12 rounded-lg font-integral text-[12px]"
                            type="submit" action="#">
                            {{ isRegister ? 'S\'INSCRIRE' : 'SE CONNECTER' }}
                        </button>
                    </div>

                    <div class="flex items-center mt-16 ml-20">
                        <p class="text-greyTextMDS">
                            ou continue avec
                        </p>
                    </div>
                </form>
            </div>
        </div>
        <div class="w-1/2 bg-black flex flex-col items-center justify-center rounded-lg mt-4 mb-4 mr-4">
            <img src="/assets/images/eggSelfieGirl.png" alt="Image" class="w-2/5 max-w-xl h-[60%] mt-12" />
            <p class="text-white font-semibold text-[40px] mt-10">Rejoins la communauté</p>
            <p class="text-[20px] font-light text-white">Et sois mis en relation en 15 secondes.</p>
        </div>
    </div>
</template>

<style>
input:focus {
    outline: none;
    box-shadow: none;
}
</style>