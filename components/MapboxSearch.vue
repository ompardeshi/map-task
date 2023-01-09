<template>
    <div ref="mapContainer"></div>
</template>

<script>
import mapboxgl from 'mapbox-gl'
const maptoken = 'pk.eyJ1IjoiZW1pbGx5MTc2IiwiYSI6ImNsYzNjZHRiajN5enQzdnFuemNxNjdlbWYifQ.cG5N0l_CfwZDVgjIC3wGfQ'
const algolia_app_id = 'C7XZ9G8VDY'
const algolia_api_key = '0320f6eb39bf150d0bf93b6bb3435cef'

export default {
  data() {
    return {
      map: null
    }
  },
  async mounted() {
    const client = algoliasearch(algolia_app_id, algolia_api_key)
    const index = client.initIndex('map_members')
    const results = await index.search('Alikee Hanhart')

    mapboxgl.accessToken = maptoken

    this.map = new mapboxgl.Map({
      container: this.$refs.mapContainer,
      style: 'mapbox://styles/mapbox/streets-v11',
      center: [0, 0],
      zoom: 1
    })

    for (const result of results.hits) {
      const marker = new mapboxgl.Marker()
        .setLngLat([result.lng, result.lat])
        .addTo(this.map)
    }
  }
}
</script>
