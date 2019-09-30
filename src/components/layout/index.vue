<template>
  <div class="layout">
    <div class="layout__info">
      <div class="header">
        <lang />
        <h1 class="header__title">
          {{ $t('headerTitle') }}
        </h1>
      </div>
      <div class="markers">
        <slot></slot>
      </div>
    </div>
    <div class="layout__map">
      <slot name="map"></slot>
    </div>
  </div>
</template>

<script>
import lang from '../lang/index.vue';

export default {
  name: 'layout',
  components: {
    lang,
  },
};
</script>

<style>
body {
  margin: 0;
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
.header .lang {
  float: right;
  padding-top: 4px;
}
.markers {
  margin: 0;
  padding: 0;
  list-style: none;
}
</style>
