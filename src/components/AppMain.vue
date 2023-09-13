<script>
import CardList from "./CardList.vue";
import bootstrap from "bootstrap/dist/css/bootstrap.css";
import axios from "axios";

export default {
  data() {
    return {
      cards: [],
      archetypes: [],
    };
  },

  components: {
    CardList,
    bootstrap,
  },

  methods: {
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
  },

  created() {
    this.fetchArchetypes();
  },
};
</script>

<template>
  <main class="mt-3 pt-5">
    <div class="w-25 mb-5 container">
      <select class="form-select">
        <option selected>Seleziona un tipo</option>
        <option
          v-for="archetype in archetypes"
          :value="archetype.archetype_name"
        >
          {{ archetype.archetype_name }}
        </option>
      </select>
    </div>

    <CardList />
  </main>
</template>

<style lang="scss" scoped>
main {
  background-color: #d48f38;
}
</style>
