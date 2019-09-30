<template>
  <p class="hint" v-if="visible">
    {{ $t('markersHint') }}
  </p>
</template>

<script>
export default {
  name: 'hint',
  props: {
    visible: Boolean,
  },
};
</script>

<style scoped>
.hint {
  font-style: italic;
  color: #999;
}
</style>
