<template>
  <div class="home">
    <ThePagination
      :pagination="pagination"
      @get-page="getPage"
    />
    <StarshipList :starships="starships" />
    <ThePagination
      :pagination="pagination"
      @get-page="getPage"
    />
  </div>
</template>

<script>
import StarshipList from "../components/StarshipList";
import ThePagination from "../components/ThePagination";

export default {
  name: "Home",
  components: {
    StarshipList,
    ThePagination,
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

        // console.log(results[0]);

        return [{ count, next, previous }, results];
      } catch (err) {
        console.log(err.message);
      }
    },
    async getPage(url) {
      try {
        const res = await fetch(url);

        const data = await res.json();

        const { count, next, previous, results } = data;

        [this.pagination, this.starships] = [
          { count, next, previous },
          results,
        ];
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
