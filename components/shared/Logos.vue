<script setup lang="ts">

</script>

<script>
export default {
    data() {
        return {
            photos: [
                { src: "/assets/images/logoNike.png" }, 
                { src: "/assets/images/logoBk.png" },
                { src: "/assets/images/logoSamsung.png" }, 
                { src: "/assets/images/logoAdidas.png" }, 
                { src: "/assets/images/logoGoogle.png" }, 
                { src: "/assets/images/logoKfc.png" }
            ]
        };
    },
};

</script>

<template>
    <div id="mother" class="bg-purpleMDS mt-[-4%]">
        <div id="childColumn" class="flex flex-col">
            <div id="logoDivRow" class="flex flex-row justify-center gap-16">
                <img v-for="photo in photos" class="mt-36 h-12 w-20 object-contain" :src="photo.src" />
            </div>
            <div id="textDivRow" class="flex flex-row justify-center mt-20 mb-60">
                <p class="flex w-[44%] justify-evenly text-2xl leading-9 font-bold">
                Infline est la plateforme numéro 1 dans la mise en relation entre les influenceurs et les marques en France. 
                Finies les recherches interminables, 
                matchez avec le profil parfait
                </p>
                
            </div>
        </div>
    </div>
</template>

<style scoped></style>