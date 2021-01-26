<!-- @format -->

<template>
  <v-app>
    <v-app-bar app color="black" dark dense flat>
      <div class="d-flex align-center">
        <h3>Vue Gradient Slider</h3>
      </div>

      <v-spacer></v-spacer>

      <v-btn
        href="https://github.com/Imgplug/vue-gradient-picker"
        target="_blank"
        text
      >
        <span class="mr-2">See Github</span>
        <v-icon>mdi-github</v-icon>
      </v-btn>
    </v-app-bar>

    <v-main>
      <Home />
    </v-main>
  </v-app>
</template>

<script>
import Home from "./components/Home";

export default {
  name: "App",

  components: {
    Home,
  },

  data: () => ({
    //
  }),
};
</script>
