<template>
    <div class="map-wrap">
        <div class="map" ref="mapContainer"></div>
    </div>
</template>

<script setup>
import { Map, MapStyle, Marker, config } from '@maptiler/sdk';
import { shallowRef, onMounted, onUnmounted, markRaw } from 'vue';
import '@maptiler/sdk/dist/maptiler-sdk.css';

const mapContainer = shallowRef(null);
const map = shallowRef(null);

onMounted(() => {
    config.apiKey = 'ysmbYpTRQA8zuUSMfopO';

    const initialState = { lng: 139.753, lat: 35.6844, zoom: 1 };

    map.value = markRaw(new Map({
        container: mapContainer.value,
        style: MapStyle.STREETS.DARK,
        center: [initialState.lng, initialState.lat],
        zoom: initialState.zoom,
        navigationControl: true,
    }));

    new Marker({ color: "#FF0000" })
        .setLngLat([139.7525, 35.6846])
        .addTo(map.value);
    
    new Marker({ color: "#00FF00" })
        .setLngLat([0, 0])
        .addTo(map.value);

}),
    onUnmounted(() => {
        map.value?.remove();
    })


</script>

<style scoped>
.map-wrap {
    position: relative;
    width: 100%;
    height: calc(100vh - 77px);
    /* calculate height of the screen minus the heading */
}

.map {
    position: absolute;
    width: 100%;
    height: 100%;
}
</style>