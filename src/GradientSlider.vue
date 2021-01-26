<!-- @format -->
<template>
  <div @mousemove="moveKnob" @mouseup="endMoveKnob" @click="addKnob">
    <div class="gradient-slider" ref="slider" :style="{ background: gradient }">
      <div
        class="gradient-slider__knob"
        v-for="(color, key) in value"
        :key="key"
        :style="{
          left: `${color.position * 100}%`,
          background: color.color,
        }"
        :ref="`knob-${key}`"
        @click="selectKnobToEdit(key, $event)"
        @mousedown="selectKnobToMove(key, $event)"
        @touchstart="selectKnobToMove(key, $event)"
      ></div>
    </div>
  </div>
</template>

<script>
const roundTwoDecimals = (num) => Math.round(num * 100) / 100;

// Width of knob
const KNOB_WIDTH = 12;

export default {
  props: {
    value: { default: () => [], type: Array },
  },
  data: () => ({
    selectedKnob: -1,
    movingKnob: {
      el: null,
      index: -1,
    },
  }),
  computed: {
    gradient() {
      const knobs = this.value;
      // Refer: https://cssgradient.io/
      const gradLines = knobs.reduce((accumulator, val, index) => {
        return (
          accumulator +
          `${val.color} ${val.position * 100}%${
            knobs.length === index + 1 ? "" : ","
          }`
        );
      }, "");

      return `linear-gradient(90deg, ${gradLines})`;
    },
  },
  methods: {
    setValue(value) {
      this.$emit("input", value);
    },
    addKnob(event) {
      // Don't add if there is a moving knob
      if (this.movingKnob.el) {
        return;
      }
      const { pageX } = event;
      const sliderRect = this.$refs.slider.getBoundingClientRect();
      const xOffset = roundTwoDecimals(
        pageX - KNOB_WIDTH / 2 - sliderRect.left
      );
      const xOffsetChange = roundTwoDecimals(xOffset / sliderRect.width);

      const knobs = [
        ...this.value,
        {
          position: xOffsetChange,
          color: "#00aaff",
        },
      ];
      // Sort by position
      knobs.sort((a, b) => a.position - b.position);

      this.setValue(knobs);
    },
    selectKnobToEdit(index, event) {
      this.selectedKnob = index;
      this.$emit("select", index);
      event.stopPropagation();
      return false;
    },
    selectKnobToMove(index, event) {
      this.movingKnob = {
        index,
        el: event.target,
      };
    },
    moveKnob(event) {
      event.preventDefault();
      event.stopPropagation();

      if (!this.movingKnob.el) {
        return;
      }
      // calculate the new cursor position:
      const { clientX } = event;
      const sliderRect = this.$refs.slider.getBoundingClientRect();
      let xOffset = roundTwoDecimals(
        clientX - KNOB_WIDTH / 2 - sliderRect.left
      );

      if (xOffset < 0) xOffset = 0;
      if (xOffset > sliderRect.width) xOffset = sliderRect.width;

      const knob = this.movingKnob.el;
      // this.movingKnob = event.target;

      knob.style.left = `${xOffset}px`;
    },
    endMoveKnob() {
      if (!this.movingKnob.el) {
        return;
      }

      const knob = this.movingKnob.el.getBoundingClientRect();
      const sliderRect = this.$refs.slider.getBoundingClientRect();
      const xOffsetChange = (knob.left - sliderRect.left) / sliderRect.width;

      if (xOffsetChange < 0 || xOffsetChange > 1) {
        return;
      }

      const knobs = this.value;
      knobs[this.movingKnob.index].position = roundTwoDecimals(xOffsetChange);

      // Sort by position
      knobs.sort((a, b) => a.position - b.position);

      this.setValue(knobs);

      this.movingKnob = {
        index: -1,
        el: null,
      };
    },
  },
};
</script>

<style lang="scss" scoped>
.gradient-slider {
  width: 100%;
  height: 20px;
  background: #e3e3e3;
  position: relative;
  margin-top: 5px;
  margin-bottom: 5px;

  &__knob {
    position: absolute;
    top: -3px;
    left: 50%;
    width: 10px;
    height: 26px;
    // border: 1px solid #434343;
    border-radius: 3px;
    cursor: pointer;
    -webkit-box-shadow: 2px 2px 5px 0px rgba(50, 50, 50, 0.55);
    -moz-box-shadow: 2px 2px 5px 0px rgba(50, 50, 50, 0.55);
    box-shadow: 2px 2px 5px 0px rgba(50, 50, 50, 0.55);
  }
}
</style>
