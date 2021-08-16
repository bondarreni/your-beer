<template>
  <v-footer padless>
    <v-col class="text-center" cols="12">
      {{ new Date().getFullYear() }} —
      <a href="https://bondarreni.github.io/cv/">Bondár Reni</a>
    </v-col>
  </v-footer>
</template>

<script>
export default {
  name: "Footer",
};
</script>

<style scoped>
footer {
  margin-top: 30px;
}
a {
  text-decoration: none !important;
}
</style>
