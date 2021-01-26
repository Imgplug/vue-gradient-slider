<!-- @format -->

# Vue Gradient Slider

<p align="center">
  <img src="https://thumbs.gfycat.com/ImpassionedOrangeDassierat-size_restricted.gif" width=400>
</p>

## Install

```bash
npm install vue-gradient-slider
```

## Usage

```html
<GradientPicker v-model="colors" @select="selectKnob" />
```

```js
export default {
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
