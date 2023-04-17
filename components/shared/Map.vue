<script setup lang="ts">
</script>

<script>
import mapboxgl from 'mapbox-gl'
import axios from 'axios'
export default {
    data() {
        return {
            accessToken: 'pk.eyJ1IjoiYnJ1bm9hY21kcyIsImEiOiJjbGU3NmI4bnAwMmczM3duYnhjdzFiYzg3In0.U1QV92f0JnBZ1oJQvgJXDQ',
            center: [6.0934836, 45.8899344],
            zoom: 12,
            markers: [],
        }
    },
    mounted() {
        this.fetchMarkers()
        this.checkAuth()
    },
    methods: {
        checkAuth() {
            const jwt = localStorage.getItem('jwt')
            if (!jwt) {
                this.$router.push('/login')
            }
        },
        async fetchMarkers() {
            const response = await axios.get('http://localhost:1337/influenceurs')
            const markers = []

            for (const marker of response.data) {
                console.log("marker", marker.address)
                const address = encodeURIComponent(marker.address)
                const url = `https://api.mapbox.com/geocoding/v5/mapbox.places/${address}.json?access_token=${this.accessToken}`
                console.log("url", url)
                const response = await axios.get(url)

                if (response.data.features.length > 0) {
                    console.log("ok")
                    const feature = response.data.features[0]
                    const longitude = feature.center[0]
                    const latitude = feature.center[1]
                    console.log("longitude", longitude)
                    console.log("latitude", latitude)
                    markers.push({ longitude, latitude })
                }
            }

            this.markers = markers
            this.initMap()
        },
        initMap() {
            mapboxgl.accessToken = this.accessToken
            const map = new mapboxgl.Map({
                container: 'mapContainer',
                style: 'mapbox://styles/mapbox/light-v10',
                center: this.center,
                zoom: this.zoom,
            })

            // Add markers to the map
            this.markers.forEach((marker) => {
                console.log("marker", marker.longitude)
                new mapboxgl.Marker()
                .setLngLat([marker.latitude, marker.longitude])
                    .addTo(map)
            })
        },
    },
}
</script>


<template>
    <div class="flex flex-col" id="mother">
        <div class="flex mt-6 ml-8 w-[100%]">
            <p class="text-[24px] font-integral text-black">INFLINE</p>
        </div>
        <div class="flex mt-2 ml-8 w-[100%]">
            <p class="text-[30px] font-bold font-integral text-black">HELLO,</p>
        </div>
        <div class="flex mt-2 ml-8 w-[100%]">
            <p>Trouve l’influenceur qu’il te faut ici !</p>
        </div>
        <div id="mapContainer"></div>
        <div class="flex mt-6 ml-8">
      <button class="bg-purpleMDS font-integral text-[12px] font-bold text-white text-center py-4 px-6 rounded-lg">
        RECHERCHER ICI 
      </button>
    </div>
    </div>
</template>


<style>
#mother{
    overflow-y: hidden;
    overflow-x: hidden;
}
#mapContainer {
    width: 100%;
    height: 70vh;
}</style>