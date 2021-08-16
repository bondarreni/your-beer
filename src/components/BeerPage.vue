<template>
  <div>
    <div class="row">
      <div class="col-lg-3 col-md-4">
        <v-btn @click="goBack">
          Back
        </v-btn>
      </div>
    </div>

    <div class="row">
      <div class="col-lg-3 col-md-4">
        <div>
          <img :src="beer.image_url" alt="team member" class="beer-image" @click="update"/>
        </div>
      </div>
      <div class="col-lg-9 col-md-8">
        <div>
          <h2>{{ beer.name }}</h2>
          <span
            ><strong>{{ beer.tagline }}</strong></span
          >
        </div>
        <div>
          <p>
            {{ beer.description }}
          </p>
        </div>

        <v-divider></v-divider>

        <div class="extraDetails">
          <h4>Details</h4>
          <div class="tableDiv">
            <v-simple-table>
              <tbody>
                <tr>
                  <td>
                    <div class="tooltip">
                      ABV
                      <span class="tooltiptext">Alcohol by volume</span>
                    </div>
                  </td>
                  <td>{{ beer.abv }}%</td>
                </tr>
                <tr>
                  <td>
                    <div class="tooltip">
                      IBU
                      <span class="tooltiptext"
                        >International Bittering Units</span
                      >
                    </div>
                  </td>
                  <td>{{ beer.ibu }}</td>
                </tr>
                <tr>
                  <td>
                    <div class="tooltip">
                      EBC
                      <span class="tooltiptext"
                        >European Brewery Convention</span
                      >
                    </div>
                  </td>
                  <td>{{ beer.ebc }}</td>
                </tr>
                <tr>
                  <td>
                    <div class="tooltip">
                      SRM
                      <span class="tooltiptext">Standard Reference Method</span>
                    </div>
                  </td>
                  <td>{{ beer.srm }}</td>
                </tr>
                <tr>
                  <td>
                    <div class="tooltip">
                      PH
                      <span class="tooltiptext">Potential of hydrogen</span>
                    </div>
                  </td>
                  <td>{{ beer.ph !== null ? beer.ph : 'n.a'}}</td>
                </tr>
              </tbody>
            </v-simple-table>
          </div>
          <v-divider></v-divider>

          <div>
            <h4>Food pairing</h4>
            <ul>
              <li v-for="item in beer.food_pairing" :key="item">
                {{ item }}
              </li>
            </ul>
          </div>
          <v-divider></v-divider>
          <h4>Brewer's tip</h4>
          <p>
            {{ beer.brewers_tips }}
          </p>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "BeerPage",
  props: {
    id: Number,
  },
  data() {
    return {
      beer: {},
    };
  },
  async created() {
    if (this.id === null) {
      let res = await fetch("https://api.punkapi.com/v2/beers/random");
      let data = await res.json();
      this.beer = data[0];
      console.log(this.beer)
    } else {
      let res = await fetch("https://api.punkapi.com/v2/beers?ids=" + this.id);
      let data = await res.json();
      this.beer = data[0];
    }

    if (this.beer.image_url === null) {
      this.beer.image_url =
        "https://i.ibb.co/pP7Rsyv/K-perny-fot-2021-08-14-17-21-24.png";
    }

    window.addEventListener("keydown", this.goBackEsc);
  },
  destroyed() {
    window.removeEventListener("keydown", this.goBackEsc);
  },
  methods: {
    goBack() {
      this.$emit("go-back");
    },
    goBackEsc(e) {
      if (e.key === "Escape") {
        this.$emit("go-back");
      }
    },
    update() {
        this.$forceUpdate();
    }
  },
};
</script>

<style scoped>
.beer-image {
  width: 10vw;
}

.v-btn {
  margin-bottom: 30px;
}

.extraDetails {
  text-align: left;
  margin-left: 10px;
}

ul {
  list-style: none;
}

ul li:before {
  content: "🍔";
}

.tableDiv {
  width: 50%;
}

h4 {
  margin-top: 10px;
}

/* Tooltip */

.tooltip {
  position: relative;
  display: inline-block;
}

.tooltip .tooltiptext {
  visibility: hidden;
  width: 200px;
  background-color: black;
  color: #fff;
  text-align: center;
  border-radius: 6px;
  padding: 5px 0;

  position: absolute;
  z-index: 1;
}

.tooltip:hover .tooltiptext {
  visibility: visible;
}
</style>
