<script setup lang="ts">

</script>

<script>
export default {
    data() {
        return {
            photos: [
                { src: "/assets/images/blackSeparationImg1.png" },
                { src: "/assets/images/blackSeparationImg2.png" },
                { src: "/assets/images/blackSeparationImg3.png" },
                { src: "/assets/images/blackSeparationImg4.png" },
                { src: "/assets/images/blackSeparationImg5.png" },
                { src: "/assets/images/blackSeparationImg6.png" }
            ]
        };
    },
};
</script>


<template>
    <div class="bg-black mt-32 h-[525px]">
        <div id="childColumn" class="">
            <div id="imageDivRow" class="">
                <!--<img v-for="photo in photos" class="h-28 w-52 object-contain" :src="photo.src" />-->
                <img src="/assets/images/blackSeparationImg1.png" alt="" class="absolute left-0 w-[250px] h-[185px] z-0">
                <img src="/assets/images/blackSeparationImg2.png" alt="" class="absolute mt-[230px] left-48 w-[250px] h-[290px]">
                <img src="/assets/images/blackSeparationImg3.png" alt="" class="absolute left-[40%] mt-[60px] w-[180px] h-[210px]">
                <img src="/assets/images/blackSeparationImg4.png" alt="" class="absolute left-[48%] mt-[408px] w-[265px] h-[117px]">
                <img src="/assets/images/blackSeparationImg5.png" alt="" class="absolute  right-8 w-[182px] h-[210px]">
                <img src="/assets/images/blackSeparationImg6.png" alt="" class="absolute right-0 mt-[348px] w-[389px] h-[175px]">
            </div>
            <div class="ml-[25%] flex justify-between max-w-[75%]">
                <div class="flex-row w-[60%] mt-[6%] ml-[-2%]">
                    <p class="font-integral text-white text-5xl mt-36 z-50 text-center relative">
                        DÉJA PLUS DE
                    </p>
                    <p class="font-integral text-purpleMDS text-5xl z-50 text-center relative">
                        250 COLLABORATIONS
                    </p>
                </div>
            </div>
        </div>
    </div>
</template>

<style></style>