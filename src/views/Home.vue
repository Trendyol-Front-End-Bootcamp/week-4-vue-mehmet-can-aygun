<template>
  <div class="home">
    <StarshipList :starships="starships" />
  </div>
</template>

<script>
import StarshipList from "../components/StarshipList";

export default {
  name: "Home",
  components: {
    StarshipList,
  },
  data() {
    return {
      starships: [],
      pagination: null,
    };
  },
  methods: {
    async getStarships() {
      try {
        const res = await fetch("https://swapi.dev/api/starships/");

        const data = await res.json();

        const { count, next, previous, results } = data;

        console.log(results[0]);

        return [{ count, next, previous }, results];
      } catch (err) {
        console.log(err.message);
      }
    },
  },
  async created() {
    [this.pagination, this.starships] = await this.getStarships();
    console.log(this.pagination);
  },
};
</script>

<style lang="scss" scoped>
// Imports
@import "../style/variables";

.home {
  padding: $py $px;
}
</style>
