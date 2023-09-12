<script>
import CardList from "./CardList.vue";
import bootstrap from "../../node_modules/bootstrap/dist/css/bootstrap.min.css";

export default {
  data() {
    return {};
  },

  components: {
    CardList,
    bootstrap,
  },
};
</script>

<template>
  <main class="mt-3 pt-5">
    <CardList />
  </main>
</template>

<style lang="scss" scoped>
main {
  background-color: #d48f38;
}
</style>
