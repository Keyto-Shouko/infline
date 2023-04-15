<script setup lang="ts">
</script>

<script>
export default {
    props: {
        isRegister: {
            type: Boolean,
            default: false
        }
    }
}
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
                <p v-else class="mb-4">Tu es déjà inscrit ? <br>Tu peux <span class="text-purpleMDS"><a href="./login">te connecter ici</a></span>
                </p>
                <form class="mt-12">
                    <div class="mb-4 relative">
                        <label class="block text-greyTextMDS text-[13px]" for="email">
                            Email
                        </label>
                        <input class="bg-transparent w-[350px] py-2 px-3 border-b-black border-transparent" id="email"
                            type="text" placeholder="Entre ton adresse e-mail" />
                    </div>
                    <div class="mb-4">
                        <label class="block text-greyTextMDS text-[13px]" for="password">
                            Mot de passe
                        </label>
                        <input class=" w-full py-2 px-3 border-b-black border-transparent" id="password" type="password"
                            placeholder="Entre ton mot de passe" />
                    </div>
                    <div v-if="isRegister" class="mb-4">
            <label class="block text-greyTextMDS text-[13px]" for="confirmPassword">
              Confirmer le mot de passe
            </label>
            <input
              class="w-full py-2 px-3 border-b-black border-transparent"
              id="confirmPassword"
              type="password"
              placeholder="Confirme ton mot de passe"
            />
          </div>
                    <div class="flex items-center justify-between mt-8">
                        <button class="bg-purpleMDS text-white font-bold py-3 px-12 rounded-lg font-integral text-[12px]"
                            type="button">
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
        <div class="w-1/2 bg-black flex items-center justify-center rounded-lg mt-4 mb-4 mr-4">
            <img src="/assets/images/eggSelfieGirl.png" alt="Image" class="w-2/5 max-w-xl" />
        </div>
    </div>
</template>

<style>
input:focus {
    outline: none;
    box-shadow: none;
}
</style>