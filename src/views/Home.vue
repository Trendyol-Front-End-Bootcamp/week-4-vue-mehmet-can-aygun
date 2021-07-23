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
    // Get all starships when the home view mounts
    async getStarships() {
      // Set Loading true to display loading animation
      this.loading = true;

      // Make the API call and return the data including starships & pagination
      // Display errors on the console if there's any
      try {
        const res = await fetch("https://swapi.dev/api/starships/");

        const data = await res.json();

        // Set loading false once the data is fetched
        this.loading = false;

        const { count, next, previous, results } = data;

        return [{ count, next, previous }, results];
      } catch (err) {
        console.log(err.message);
      }
    },
    // Get next or previous page
    async getPage(url) {
      // Set Loading true to display loading animation
      this.loading = true;

      // Make the API call and set state with the newly fetched data
      // Display errors on the console if there's any
      try {
        const res = await fetch(url);

        const data = await res.json();

        // Set loading false once the data is fetched
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
    // Search starships that match with the search term
    async searchStarship(term) {
      // Set Loading true to display loading animation
      this.loading = true;

      // Make the API call and set state with the search results
      // Display errors on the console if there's any
      try {
        const res = await fetch(
          `https://swapi.dev/api/starships/?search=${term}`
        );

        const data = await res.json();

        // Set loading false once the data is fetched
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
  // Call function to get all starships when the Home view is created
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
