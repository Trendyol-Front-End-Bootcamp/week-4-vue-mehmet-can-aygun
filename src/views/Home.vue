<template>
  <main class="home">
    <TheSearch @search-starship="searchStarship" />
    <div
      class="loading"
      v-if="loading"
    >
      <TheLoading />
    </div>
    <div
      class="home-container"
      v-else
    >
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
  </main>
</template>

<script>
import StarshipList from "../components/StarshipList";
import ThePagination from "../components/ThePagination";
import TheSearch from "../components/TheSearch";
import TheLoading from "../components/TheLoading";

export default {
  name: "Home",
  components: {
    StarshipList,
    ThePagination,
    TheSearch,
    TheLoading,
  },
  data() {
    return {
      starships: [],
      pagination: null,
      loading: false,
    };
  },
  methods: {
    async getStarships() {
      this.loading = true;

      try {
        const res = await fetch("https://swapi.dev/api/starships/");

        const data = await res.json();

        this.loading = false;

        const { count, next, previous, results } = data;

        return [{ count, next, previous }, results];
      } catch (err) {
        console.log(err.message);
      }
    },
    async getPage(url) {
      this.loading = true;

      try {
        const res = await fetch(url);

        const data = await res.json();

        this.loading = false;

        const { count, next, previous, results } = data;

        [this.pagination, this.starships] = [
          { count, next, previous },
          results,
        ];
      } catch (err) {
        console.log(err.message);
      }
    },
    async searchStarship(term) {
      this.loading = true;

      try {
        const res = await fetch(
          `https://swapi.dev/api/starships/?search=${term}`
        );

        const data = await res.json();

        this.loading = false;

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
