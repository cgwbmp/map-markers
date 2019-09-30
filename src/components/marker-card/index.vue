<template>
  <div
    class="marker"
    :class="{ 'marker--active': isActive }"
  >
    <button class="marker__button" @click="click">
      <h4 class="marker__title">
        {{ title }}
      </h4>
      <p class="marker__info">
        {{ coords }}
      </p>
    </button>
  </div>
</template>

<script>
export default {
  name: 'marker-card',
  props: {
    id: String,
    title: String,
    coords: [Number, Number],
    isActive: Boolean,
  },
  methods: {
    click() {
      this.$emit('click');
    },
  },
};
</script>

<style scoped>
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
</style>
