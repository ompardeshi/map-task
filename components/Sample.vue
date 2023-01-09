<template>
    <div ref="mapContainer">
        <ais-index :app-id="'C7XZ9G8VDY'" :api-key="'0320f6eb39bf150d0bf93b6bb3435cef'"
            :index-name="'map_members'">
            <ais-search-box />
            <ais-results>
                <template v-slot="{ result }">
                    <h2>{{ result.fullName }}</h2>
                    <div ref="marker" v-bind:data-lng="result.lng" v-bind:data-lat="result.lat"></div>
                </template>
            </ais-results>
        </ais-index>
    </div>
</template>


<script>
import algoliasearch from 'algoliasearch'
import mapboxgl from 'mapbox-gl'
import { defineComponent } from 'vue'
import { AisIndex, AisSearchBox, AisResults } from 'vue-instantsearch'

const maptoken = 'pk.eyJ1IjoiZW1pbGx5MTc2IiwiYSI6ImNsYzNjZHRiajN5enQzdnFuemNxNjdlbWYifQ.cG5N0l_CfwZDVgjIC3wGfQ'
const algolia_app_id = 'C7XZ9G8VDY'
const algolia_api_key = '0320f6eb39bf150d0bf93b6bb3435cef'


export default defineComponent({
    components: {
        AisIndex,
        AisSearchBox,
        AisResults
    },
    data() {
        return {
            map: null
        }
    },
    async mounted() {
        mapboxgl.accessToken = maptoken

        this.map = new mapboxgl.Map({
            container: this.$refs.mapContainer,
            style: 'mapbox://styles/mapbox/streets-v11',
            center: [0, 0],
            zoom: 1
        })

        const markers = this.$refs.marker
        for (const marker of markers) {
            new mapboxgl.Marker()
                .setLngLat([marker.dataset.lng, marker.dataset.lat])
                .addTo(this.map)
        }
    }
})

</script>
