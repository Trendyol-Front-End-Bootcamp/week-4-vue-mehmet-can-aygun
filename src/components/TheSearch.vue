<template>
  <div class="search-container">
    <form
      className="search-form"
      @submit.prevent="onSubmit"
    >
      <div className="input-group">
        <label>Search Term</label>
        <input
          v-model="searchTerm"
          type="search"
          placeholder="Enter a starship name or a model"
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
      searchTerm: "",
    };
  },
  methods: {
    onSubmit() {
      this.$emit("search-starship", this.searchTerm);
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

      input {
        height: 36px;
        padding: 0 8px;
        font-size: 16px;
        border: none;
        outline: none;
        border-radius: 4px;
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
        border-radius: 4px;
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