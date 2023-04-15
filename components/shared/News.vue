<script setup lang="ts">
</script>

<script>
export default {
    data() {
        return {
            news: [
                { img: "/assets/images/unzoomedSelfieGirl.png", title: 'Trouver l’influenceur parfait pour votre marque', date: '4 mars 2022', isCenter: false },
                { img: "/assets/images/zoomedSelfieGirl.png", title: '50 nouvelles influenceuses rejoigent la plateforme', date: '7 mars 2022', isCenter: true },
                { img: "/assets/images/unzoomedSelfieGirl.png", title: 'Instagram investit 100 millions d’euros dans Infline', date: '1 juin 2022', isCenter: false },
            ]
        };
    },
};
</script>

<template>
  <div class="flex flex-col mt-8">
    <div class="flex flex-row">
      <p class="font-bold font-integral text-[55px] leading-[72px] ml-44">
        LES NEWS
      </p>
    </div>
    <div class="flex flex-row flex-wrap">
      <div
        v-for="(oneNews, index) in news"
        :key="index"
        class="flex-1 m-4 max-w-[400px] mx-auto"
      >
        <div class="mt-8">
          <p class="font-semibold mt-4 pb-6 border-b-2 border-black">
            {{ oneNews.date }}
          </p>
          <p class="font-semibold mt-4 mb-6 w-52">{{ oneNews.title }}</p>
          <img :class="[oneNews.isCenter ? 'h-full object-contain' : 'h-96 w-full object-cover']" :src="oneNews.img" alt="" />
        </div>
      </div>
    </div>
  </div>
</template>



<style></style>