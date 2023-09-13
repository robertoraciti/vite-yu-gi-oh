<script>
import axios from "axios";
import Card from "./Card.vue";
import bootstrap from "../../node_modules/bootstrap/dist/css/bootstrap.min.css";

export default {
  data() {
    return {
      cards: [],
    };
  },

  components: {
    Card,
    bootstrap,
  },

  methods: {
    fetchCards() {
      axios
        .get("https://db.ygoprodeck.com/api/v7/cardinfo.php?num=40&offset=0")
        .then((result) => {
          const cardsData = result.data.data.map((card) => {
            const { name, card_images, archetype } = card;
            return { name, card_images, archetype };
          });
          this.cards = cardsData;
        });
    },
  },

  created() {
    this.fetchCards();
  },
};
</script>

<template>
  <section class="container">
    <div class="row g-2 cards-container">
      <div class="text-center card-element" v-for="card in cards">
        <img :src="card.card_images[0].image_url" alt="" srcset="" />
        <p class="title">{{ card.name }}</p>
        <p>{{ card.archetype }}</p>
      </div>
    </div>
  </section>
  <!-- <Card /> -->
</template>

<style lang="scss" scoped>
section {
  width: 70%;
  margin: auto;
  background-color: white;

  .cards-container {
    width: 90%;
    margin: auto;
  }
}
.card-element {
  width: 20%;
  border: 1px solid black;
  background-color: #d48f38;

  .title {
    color: white;
  }
}
img {
  width: 170px;
}
</style>
