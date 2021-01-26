<!-- @format -->

# Vue Gradient Slider

<p align="center">
  <img src="https://thumbs.gfycat.com/ImpassionedOrangeDassierat-size_restricted.gif" width=400>
</p>

## Install

```bash
npm install vue-gradient-slider
# or
yarn add vue-gradient-slider
```

## Demo

See [Demo Site](https://vue-gradient-slider.vercel.app/)

## Usage

```html
<GradientSlider v-model="colors" @select="selectKnob" />
```

```js
import GradientSlider from 'vue-gradient-slider'

export default {
  components: {
    GradientSlider
  },
  data: () => ({
    selectedKnob: 0,
    colors: [
      {
        position: 0.12,
        color: "#FF00AA",
      },
      {
        position: 0.46,
        color: "#A300FF",
      },
      {
        position: 0.84,
        color: "#00AAFF",
      },
    ],
  }),
  methods: {
    selectKnob(value) {
      this.selectedKnob = value;
    },
  },
};
```
