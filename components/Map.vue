<template>
    <div ref="mapContainer"></div>
</template>

<script>
import mapboxgl from 'mapbox-gl'
const maptoken = 'pk.eyJ1IjoiZW1pbGx5MTc2IiwiYSI6ImNsYzNjZHRiajN5enQzdnFuemNxNjdlbWYifQ.cG5N0l_CfwZDVgjIC3wGfQ'
mapboxgl.accessToken = maptoken

export default {
data() {
    return {
    map: null
    }
},
mounted() {
    this.map = new mapboxgl.Map({
    container: this.$refs.mapContainer,
    style: 'mapbox://styles/mapbox/streets-v11',
    center: [0, 0],
    zoom: 1
    })
}
}
</script>
