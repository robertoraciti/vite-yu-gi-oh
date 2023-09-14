<script>
import bootstrap from "bootstrap/dist/css/bootstrap.css";
import axios from "axios";

export default {
  data() {
    return {
      cards: [],
      archetypes: [],
      apiUri: "https://db.ygoprodeck.com/api/v7/cardinfo.php?num=40&offset=0",
      uriFilter: "https://db.ygoprodeck.com/api/v7/cardinfo.php?archetype=",
      selectedData: "",
    };
  },

  components: {
    bootstrap,
  },

  methods: {
    fetchCards(endpoint) {
      axios.get(endpoint).then((result) => {
        const cardsData = result.data.data.map((card) => {
          const { name, card_images, archetype } = card;
          return { name, card_images, archetype };
        });
        this.cards = cardsData;
      });
    },

    fetchArchetypes() {
      axios
        .get("https://db.ygoprodeck.com/api/v7/archetypes.php")
        .then((result) => {
          const archetypes = result.data.map((archetype) => {
            const { archetype_name } = archetype;
            return { archetype_name };
          });
          this.archetypes = archetypes;
        });
    },

    filter(arch) {
      this.fetchCards(this.uriFilter + arch);
      console.log(this.uriFilter + arch);
    },
  },

  created() {
    this.fetchCards(this.apiUri);
    this.fetchArchetypes();
  },
};
</script>

<template>
  <main class="mt-3 pt-5">
    <div class="w-25 mb-5 container">
      <select
        v-model="selectedData"
        @change="filter(selectedData)"
        class="form-select"
      >
        <option selected>Seleziona un tipo</option>
        <option
          v-for="archetype in archetypes"
          :value="archetype.archetype_name"
        >
          {{ archetype.archetype_name }}
        </option>
      </select>
    </div>

    <section class="container">
      <div class="row g-2 cards-container">
        <div class="text-center card-element" v-for="card in cards">
          <img :src="card.card_images[0].image_url" alt="" srcset="" />
          <p class="title">{{ card.name }}</p>
          <p>{{ card.archetype }}</p>
        </div>
      </div>
    </section>
  </main>
</template>

<style lang="scss" scoped>
main {
  background-color: #d48f38;
}
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
