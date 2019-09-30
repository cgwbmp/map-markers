<template>
  <layout>
    <hint :visible="!markers.length" />
    <marker-card
      v-for="marker in markers"
      :key="marker.id"
      :title="marker.title"
      :coords="marker.coords"
      :isActive="marker.id === activeMarker"
      @click="setMapCenter(marker.coords)"
    />
    <template v-slot:map>
      <yandex-map
        class="map"
        :coords="mapCenter"
        :zoom="mapZoom"
        :controls="mapControls"
        :settings="{ lang: $i18n.locale }"
        @click="onMapClick"
      >
        <ymap-marker
          v-for="marker in markers"
          :key="marker.id"
          :marker-id="marker.id"
          :coords="marker.coords"
          :callbacks="{ click: () => setActiveMarker(marker.id) }"
        />
      </yandex-map>
    </template>
  </layout>
</template>

<script>
import { yandexMap, ymapMarker } from 'vue-yandex-maps';
import layout from './components/layout/index.vue';
import markerCard from './components/marker-card/index.vue';
import hint from './components/hint/index.vue';

export default {
  name: 'app',
  components: {
    yandexMap,
    ymapMarker,
    layout,
    markerCard,
    hint,
  },
  data: () => ({
    mapCenter: [55.75, 37.62],
    mapZoom: 14,
    mapControls: ['searchControl', 'zoomControl'],
    markers: [],
    activeMarker: null,
  }),
  methods: {
    onMapClick(event) {
      const coords = event.get('coords');
      const index = this.markers.length + 1;
      const newMarker = {
        id: `marker-${index}`,
        title: `Marker ${index}`,
        coords,
      };
      this.markers = [].concat(this.markers, newMarker);
      this.activeMarker = null;
    },
    setMapCenter(coords) {
      this.mapCenter = coords;
    },
    setActiveMarker(markerId) {
      this.activeMarker = markerId;
    },
  },
};
</script>

<style>
.map {
  width: 100%;
  height: 100%;
}
</style>
