<template>
  <v-app-bar app elevate-on-scroll color="white">
    <div class="d-flex align-center">
      <v-img
        alt="Vuetify Logo"
        class="shrink mr-2"
        contain
        src="../assets/logo.png"
        transition="scale-transition"
        width="40"
      />
    </div>

    <v-app-bar-title> Your<strong>Beer</strong> </v-app-bar-title>

    <v-spacer></v-spacer>

    <v-btn
      v-if="status === 0"
      target="_blank"
      text
      @click="$emit('get-random-beer')"
    >
      <span class="mr-2">Give me a beer!</span>
    </v-btn>
  </v-app-bar>
</template>

<script>
export default {
  name: "Header",
  props: {
    status: Number,
  },
};
</script>
