<!-- @format -->

<template>
  <div>
    <v-card class="pa-2" outlined tile>
      <h5>Gradient Slider</h5>
      <GradientPicker v-model="colors" @select="selectKnob"></GradientPicker>
    </v-card>
    <v-card class="pa-2" outlined tile>
      <h5>Third party color picker</h5>
      <br />
      <v-color-picker
        dot-size="25"
        swatches-max-height="200"
        mode="hexa"
        :value="selectedColor"
        @input="selectNewColor"
      ></v-color-picker>
    </v-card>
  </div>
</template>

<script>
import GradientPicker from "../../../src/GradientPicker";
export default {
  components: {
    GradientPicker,
  },
  data: () => ({
    selectedKnob: 0,
    colors: [
      {
        position: 0.4,
        color: "#ff00aa",
      },
      {
        position: 0.6,
        color: "#00aaff",
      },
    ],
  }),
  computed: {
    selectedColor() {
      return this.colors[this.selectedKnob].color;
    },
  },
  watch: {
    colors() {
      this.$emit("change", this.colors);
    },
  },
  mounted() {
    this.$emit("change", this.colors);
  },
  methods: {
    selectKnob(value) {
      console.log(value);
      this.selectedKnob = value;
    },
    selectNewColor(val) {
      this.colors[this.selectedKnob].color = val;
    },
  },
};
</script>

<style lang="scss" scoped></style>
