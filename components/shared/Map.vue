<script setup lang="ts">
</script>

<script>
import mapboxgl from 'mapbox-gl'
import axios from 'axios'
import 'mapbox-gl/dist/mapbox-gl.css'
export default {
    data() {
        return {
            isFetching: true,
            user: null,
            accessToken: 'pk.eyJ1IjoiYnJ1bm9hY21kcyIsImEiOiJjbGU3NmI4bnAwMmczM3duYnhjdzFiYzg3In0.U1QV92f0JnBZ1oJQvgJXDQ',
            center: [6.0934836, 45.8899344],
            zoom: 12,
            markers: [],
            popups: [],
        }
    },
    mounted() {
        this.fetchMarkers()
        this.checkAuth()
    },
    methods: {
        async checkAuth() {
            try {
                const jwt = localStorage.getItem('jwt')
                if (!jwt) {
                    this.$router.push('/login')
                }
                const userDetails = localStorage.getItem('user')
                if(!userDetails) {
                    this.$router.push('/login')
                }
                this.user = JSON.parse(userDetails)
                return this.isFetching = false
            } catch (error) {
                this.$router.push('/login');
            }
        },
        async fetchMarkers() {
            const responseInfluencers = await axios.get('http://localhost:1337/influenceurs')
            const markers = []

            for (const marker of responseInfluencers.data) {
                const pseudo = marker.Pseudo
                const address = encodeURIComponent(marker.address)
                const url = `https://api.mapbox.com/geocoding/v5/mapbox.places/${address}.json?access_token=${this.accessToken}`
                const responseAddress = await axios.get(url)

                if (responseAddress.data.features.length > 0) {
                    
                    const feature = responseAddress.data.features[0]
                    const fullAddress = feature.place_name
                    const longitude = feature.center[0]
                    const latitude = feature.center[1]
                    markers.push({ longitude, latitude, fullAddress, pseudo })
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
            this.markers.forEach((marker, index) => {
                console.log(marker.pseudo)
                new mapboxgl.Marker()
                    .setLngLat([marker.longitude, marker.latitude])
                    .setPopup(new mapboxgl.Popup({ offset: 25 }) // add popups
                                .setHTML(
                                    `<div class= w-[120px] h-[120px]>`
                                    + `<img class="w-[120px] h-[120px] object-cover" src="/assets/images/selfieGirl.png" alt=""/>` 
                                    + `<p>${marker.pseudo}</p>`
                                    +`</div>`

                                )
                            )
                    .addTo(map)
            })
        },
    },
}
</script>


<template>
    <div class="flex flex-col" id="mother" v-if="!isFetching">
        <div class="flex mt-6 ml-8 w-[100%]">
            <p class="text-[24px] font-integral text-black">INFLINE</p>
        </div>
        <div class="flex mt-2 ml-8 w-[100%]">
            <p class="text-[30px] font-bold font-integral text-black">HELLO {{ user['username'] }},</p>
        </div>
        <div class="flex mt-2 ml-8 w-[100%]">
            <p>Trouve l’influenceur qu’il te faut ici !</p>
        </div>
        <div id="mapContainer" class="border-black border-solid border-2"></div>
        <div class="flex mt-6 ml-8">
            <button class="bg-purpleMDS font-integral text-[12px] font-bold text-white text-center py-4 px-6 rounded-lg">
                RECHERCHER ICI
            </button>
        </div>
    </div>
</template>


<style>
#mother {
    overflow-y: hidden;
    overflow-x: hidden;
}

#mapContainer {
    width: 100%;
    height: 70vh;
}
</style>