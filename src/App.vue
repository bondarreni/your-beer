<template>
  <v-app>
    <Header @get-random-beer="getRandomBeer" :status="this.status" />

    <div v-if="status === 0">
      <Category @category-click="categoryClick" />
      <Sorting
        :category="this.category"
        @sorting-click="sortingClick"
        @input-change="inputChange"
      />
      <BeerList
        :category="this.category"
        :sorting="this.sorting"
        :inputText="this.inputText"
        @beer-click="beerClick"
      />
    </div>
    <div v-if="status === 1">
      <BeerPage :id="this.beerId" @go-back="goBack" />
    </div>

    <Footer />
  </v-app>
</template>

<script>
import Header from "./components/Header.vue";
import BeerList from "./components/BeerList.vue";
import Footer from "./components/Footer.vue";
import Category from "./components/Category.vue";
import Sorting from "./components/Sorting.vue";
import BeerPage from "./components/BeerPage.vue";

export default {
  name: "App",
  components: {
    Header,
    Category,
    Sorting,
    BeerList,
    BeerPage,
    Footer,
  },
  data() {
    return {
      category: "abv",
      sorting: null,
      inputText: "",
      status: 0, //0-main page, 1-beer details
      beerId: null,
    };
  },
  methods: {
    categoryClick(cat) {
      this.category = cat;
      this.sorting = null;
    },
    sortingClick(id) {
      if (this.sorting === id) {
        this.sorting = null;
      } else {
        this.sorting = id;
      }
    },
    inputChange(text) {
      this.inputText = text;
    },
    beerClick(id) {
      this.status = 1;
      this.beerId = id;
    },
    goBack() {
      this.status = 0;
      this.beerId = null;
    },
    getRandomBeer() {
      this.status = 1;
      this.beerId = null;
    },
  },
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
  padding: 60px;
}

@media screen and (max-width: 500px) {
  #app { 
      padding: 10px;
    }
}
</style>
