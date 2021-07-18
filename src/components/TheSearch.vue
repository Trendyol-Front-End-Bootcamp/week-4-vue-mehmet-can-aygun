<template>
  <div class="search-container">
    <form
      className="search-form"
      @submit.prevent="onSubmit"
    >
      <div className="input-group">
        <label>Search Parameter</label>
        <select v-model="searchParam">
          <option value="name">Name</option>
          <option value="model">Model</option>
        </select>
      </div>
      <div className="input-group">
        <label>Search Term</label>
        <input
          v-model="searchTerm"
          type="search"
          placeholder="Enter a search term"
        >
      </div>
      <div className="input-group btn">
        <button>
          Search
        </button>
      </div>
    </form>
  </div>
</template>

<script>
export default {
  name: "TheSearch",
  data() {
    return {
      searchParam: "name",
      searchTerm: "",
    };
  },
  methods: {
    onSubmit() {
      const searchObj = {
        param: this.searchParam,
        term: this.searchTerm,
      };

      this.$emit("search-starship", searchObj);
    },
  },
};
</script>

<style lang="scss" scoped>
// Imports
@import "../style/variables";

.search-container {
  margin-bottom: 30px;

  .search-form {
    display: flex;
    justify-content: space-between;
    gap: 20px;

    .input-group {
      flex: 1;
      display: flex;
      flex-direction: column;

      label {
        margin-bottom: 8px;
        font-size: 13px;
      }

      input,
      select {
        height: 36px;
        padding: 0 8px;
        font-size: 16px;
        border: none;
        outline: none;
      }
    }

    .input-group.btn {
      align-self: flex-end;

      button {
        height: 36px;
        border: none;
        font-size: 16px;
        background-color: $color-primary;
        color: $color-dark-gray;
        font-weight: bold;
        text-transform: uppercase;
        cursor: pointer;
      }

      button:hover {
        background-color: darken($color-primary, 10);
      }
    }
  }
}

// Media Queries
@media (max-width: 768px) {
  .search-container .search-form {
    flex-direction: column;
    gap: 10px;

    .input-group.btn {
      align-self: stretch;
      margin-top: 10px;
    }
  }
}
</style>