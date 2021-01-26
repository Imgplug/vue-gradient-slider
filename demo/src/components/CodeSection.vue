<!-- @format -->

<template>
  <v-card class="pa-2" outlined tile>
    <div class="code-section">
      <pre v-text="formatted"></pre>
    </div>
  </v-card>
</template>

<script>
export default {
  props: {
    code: { default: () => ({}), type: Object },
  },
  computed: {
    formatted() {
      return JSON.stringify(this.code, null, 2);
    },
  },
};
</script>

<style lang="scss">
.code-section {
  background: #eaeaea;
  padding: 40px 10px;
  height: 450px;
  overflow: auto;
}
</style>
