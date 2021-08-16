<template>
  <div class="row">
    <div class="column" v-for="beer in beers" :key="beer.id + Math.random()">
      <v-lazy
        :options="{
          threshold: 0.5,
        }"
        min-height="200"
        transition="fade-transition"
      >
        <Beer
          :id="beer.id"
          :name="beer.name"
          :tagline="beer.tagline"
          :abv="beer.abv"
          :ibu="beer.ibu"
          :ebc="beer.ebc"
          :imgUrl="beer.image_url"
          @beer-click="beerClick"
        />
      </v-lazy>
    </div>
  </div>
</template>

<script>
import Beer from "./Beer.vue";

export default {
  name: "BeerList",
  components: {
    Beer,
  },
  props: {
    category: String,
    sorting: Number,
    inputText: String,
  },
  data() {
    return {
      beers: [],
      params: {
        abv: {
          0: "abv_lt=4.5",
          1: "abv_gt=4.4&abv_lt=7.6",
          2: "abv_gt=7.5",
        },
        ibu: {
          0: "ibu_lt=50",
          1: "ibu_gt=49.4&ibu_lt=66",
          2: "ibu_gt=65",
        },
        ebc: {
          0: "ebc_lt=25",
          1: "ebc_gt=24&ebc_lt=51",
          2: "ebc_gt=50",
        },
      },
    };
  },
  async created() {
    this.controller = new AbortController();
    this.signal = this.controller.signal;

    const pages = [1, 2, 3, 4, 5];
    for (const page in pages) {
      let res = await fetch(
        "https://api.punkapi.com/v2/beers?page=" + pages[page] + "&per_page=80",
        this.signal
      );
      let data = await res.json();

      this.beers = this.beers.concat(data);
    }
  },
  watch: {
    category: function() {
      this.onChange();
    },
    sorting: function() {
      this.onChange();
    },
    inputText: function() {
      this.onChange();
    },
  },
  methods: {
    async onChange() {
      this.controller.abort();
      this.beers = [];
      const pages = [1, 2, 3, 4, 5];
      let url = "https://api.punkapi.com/v2/beers?per_page=80";
      if (this.sorting !== null) {
        url = url + "&" + this.params[this.category][this.sorting];
      }
      url = url + "&page=";

      for (const page in pages) {
        let res = await fetch(url + pages[page], this.signal);
        let data = await res.json();

        this.beers = this.beers.concat(data);
      }
      if (this.inputText !== "") {
        const result = this.beers.filter((beer) => {
          return beer.name.toLowerCase().includes(this.inputText.toLowerCase());
        });
        this.beers = result;
      }
      //console.log(this.beers)
    },

    beerClick(id) {
      this.$emit("beer-click", id);
    },
  },
};
</script>

<style scoped>
.beer-img {
  display: block;
  width: auto;
  max-height: 200px;
  object-fit: contain;
  display: inline-block;
}

* {
  box-sizing: border-box;
}

body {
  font-family: Arial, Helvetica, sans-serif;
}


.column {
  float: left;
  width: 25%;
  padding: 0 10px;
}


.row {
  margin: 0 -5px;
  padding: 10px;
}

.row:after {
  content: "";
  display: table;
  clear: both;
}

@media screen and (max-width: 600px) {
  .column {
    width: 100%;
    display: block;
    margin-bottom: 20px;
  }
}
</style>
