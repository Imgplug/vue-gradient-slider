<!-- @format -->

<template>
  <v-container>
    <v-row justify="center">
      <v-col md="4">
        <ColorSection @change="code = $event"></ColorSection>
      </v-col>
      <v-col md="8">
        <CodeSection :code="this.code"></CodeSection>
      </v-col>
    </v-row>
  </v-container>
</template>

<script>
import ColorSection from "./ColorSection";
import CodeSection from "./CodeSection";

export default {
  components: {
    ColorSection,
    CodeSection,
  },
  data: () => ({
    code: {},
  }),
};
</script>

<style lang="scss" scoped></style>
