<template>
  <div class="lang">
    <select v-model="$i18n.locale">
      <option
        v-for="(lang, i) in langs"
        :key="`Lang${i}`"
        :value="lang"
      >
        {{ lang }}
      </option>
    </select>
  </div>
</template>

<script>
export default {
  name: 'lang',
  data() {
    return { langs: ['en', 'ru'] };
  },
};
</script>
