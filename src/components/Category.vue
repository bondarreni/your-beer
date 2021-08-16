<template>
  <v-responsive >
  <div class="pickerDiv">
    <h1>Find Your Beer</h1>
    <p>
      Choose the category by which you want to sort the beers. <br />
    </p>

    <v-tabs background-color="transparent" color="basil" grow>
      <v-tabs-slider color="black"></v-tabs-slider>

      <v-tab class="cat-tab" @click="categoryClick('abv')"> ABV </v-tab>
      <v-tab class="cat-tab" @click="categoryClick('ibu')"> IBU </v-tab>
      <v-tab class="cat-tab" @click="categoryClick('ebc')"> EBC </v-tab>
    </v-tabs>
  </div>
  </v-responsive>
</template>

<script>
export default {
  name: "Category",
  methods: {
    categoryClick(cat) {
      this.$emit("category-click", cat);
    },
  },
};
</script>

<style scoped>
.pickerDiv {
  width: 70%;
  text-align: center;
  margin: auto;
  margin-bottom: 50px;
  background-color: rgb(247, 203, 86);
  border-radius: 25px;
  padding: 10px;
}

.pickerDiv h1 {
  font-size: 7vw;
}

.pickerDiv p {
  font-size: 2vw;
}

.v-tabs-slider {
  width: 80%;
  margin: auto;
}

@media screen and (max-width: 500px) {
    .pickerDiv { 
        width: 90%;
    }
    .v-tab {
        min-width: 0;
    }
    .pickerDiv p {
        font-size: 4vw;
    }
}

</style>
