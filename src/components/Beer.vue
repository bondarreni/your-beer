<template>
  <div class="card" @click="goToBeer(id)">
    <h3>{{ name }}</h3>
    <p>{{ abv }}%</p>
    <p>{{ tagline }}</p>
    <img :src="imgUrl !== null ? imgUrl : imgDefault" class="beer-img" />
  </div>
</template>

<script>
export default {
  name: "Beer",
  props: {
    id: Number,
    name: String,
    tagline: String,
    abv: Number,
    ibu: Number,
    ebc: Number,
    imgUrl: String,
  },
  data() {
    return {
      imgDefault:
        "https://i.ibb.co/pP7Rsyv/K-perny-fot-2021-08-14-17-21-24.png",
    };
  },
  methods: {
    goToBeer(id) {
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

.card {
  text-overflow: ellipsis;
  white-space: nowrap;
  overflow: hidden;
  padding: 16px;
  text-align: center;
  border-radius: 35px;
  margin-bottom: 30px;
}

.card:hover {
  background-color: rgba(251, 231, 185, 0.884);
  transition: 0.5s;
  cursor: pointer;
}
</style>
