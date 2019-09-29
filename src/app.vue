<template>
  <div id="app" class="layout">
    <div class="layout__info">
      <div class="header">
        <h1 class="header__title">
          Markers
        </h1>
      </div>
      <p class="hint" v-if="!markers.length">
        Click on map for adding new marker
      </p>
      <ul class="markers">
        <li
          class="markers__item marker"
          v-for="marker in markers"
          :key="marker.id"
          :class="{ 'marker--active': (marker.id === activeMarker) }"
        >
          <button class="marker__button" @click="setMapCenter(marker.coords)">
            <h4 class="marker__title">
              {{ marker.name }}
            </h4>
            <p class="marker__info">
              {{ marker.coords }}
            </p>
          </button>
        </li>
      </ul>
    </div>
    <div class="layout__map">
      <yandex-map
        class="map"
        :coords="mapCenter"
        :zoom="mapZoom"
        :controls="mapControls"
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
    </div>
  </div>
</template>

<script>
import { yandexMap, ymapMarker } from 'vue-yandex-maps';

export default {
  name: 'app',
  components: {
    yandexMap,
    ymapMarker,
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
      const marker = {
        id: `marker-${index}`,
        name: `Marker ${index}`,
        coords,
      };
      this.markers = [].concat(this.markers, marker);
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
body {
  margin: 0;
}
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}
.layout {
  display: flex;
  width: 100%;
}
.layout__info {
  width: 320px;
  max-height: 100vh;
  overflow: auto;
}
.layout__map {
  flex-grow: 1;
}
.header {
  padding: 12px;
  background-color: #ddd;
}
.header__title {
  margin: 0;
  font-size: 24px;
}
.hint {
  font-style: italic;
  color: #999;
}
.markers {
  margin: 0;
  padding: 0;
  list-style: none;
}
.markers__item {
  border-bottom: 1px solid #ddd;
}
.marker__button {
  display: block;
  width: 100%;
  border: 0;
  padding: 12px;
  background: none;
  text-align: left;
  cursor: pointer;
}
.marker__title {
  margin: 0;
  font-size: 16px;
}
.marker__info {
  margin: 4px 0 0;
  font-size: 12px;
  color: #999;
}
.marker--active {
  background-color: #dafaff;
}
.map {
  width: 100%;
  height: 100vh;
}
</style>
