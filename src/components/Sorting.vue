<template>
  <div>
    <h2>
      {{
        category === "abv"
          ? "Alcohol by volume"
          : category === "ibu"
          ? "International Bitterness Units"
          : "European Brewery Convention"
      }}
    </h2>
    <v-btn
      value="left"
      @click="sortClick(0)"
      color="white"
      :class="activeBtn === 0 ? 'active-btn' : ''"
    >
      {{ category === "abv" ? abv[0] : category === "ibu" ? ibu[0] : ebc[0] }}
    </v-btn>

    <v-btn
      value="center"
      @click="sortClick(1)"
      color="white"
      :class="activeBtn === 1 ? 'active-btn' : ''"
    >
      {{ category === "abv" ? abv[1] : category === "ibu" ? ibu[1] : ebc[1] }}
    </v-btn>

    <v-btn
      value="right"
      @click="sortClick(2)"
      color="white"
      :class="activeBtn === 2 ? 'active-btn' : ''"
    >
      {{ category === "abv" ? abv[2] : category === "ibu" ? ibu[2] : ebc[2] }}
    </v-btn>

    <v-container>
      <v-text-field color="black" @input="textChange">
        <template v-slot:label>
          Search for beer
          <v-icon style="vertical-align: middle"></v-icon>
        </template>
      </v-text-field>
    </v-container>
  </div>
</template>

<script>
export default {
  name: "Sorting",
  props: {
    category: String,
  },
  data() {
    return {
      abv: {
        0: "< 4.5%",
        1: "4.5% - 7.5%",
        2: "7.5% <;",
      },
      ibu: {
        0: "< 50",
        1: "50 - 65",
        2: "65 <;",
      },
      ebc: {
        0: "< 25",
        1: "25 - 50",
        2: "50 <;",
      },
      activeBtn: null,
    };
  },
  methods: {
    sortClick(id) {
      this.$emit("sorting-click", id);
      if (this.activeBtn !== id) {
        this.activeBtn = id;
      } else {
        this.activeBtn = null;
      }
    },
    textChange(text) {
      this.$emit("input-change", text);
    },
  },
  watch: {
    category: function() {
      this.activeBtn = null;
    },
  },
};
</script>

<style scoped>
.container {
  width: 70%;
}

.active-btn {
  background-color: rgb(218, 218, 218) !important;
}

@media screen and (max-width: 500px) {
    h2 { 
        font-size: 6vw;
    }
}
</style>
