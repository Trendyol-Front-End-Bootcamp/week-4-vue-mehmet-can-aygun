<template>
  <div
    v-if="pagination"
    class="pagination"
  >
    <button
      v-if="pagination.previous"
      @click="$emit('get-page', pagination.previous)"
    ><i class="fas fa-chevron-left"></i> Previous</button>
    <button
      v-if="pagination.next"
      @click="$emit('get-page', pagination.next)"
    >Next <i class="fas fa-chevron-right"></i></button>
  </div>
</template>

<script>
export default {
  name: "ThePagination",
  props: {
    pagination: Object,
  },
};
</script>

<style lang="scss" scoped>
// Import
@import "../style/variables";

.pagination {
  width: 100%;
  height: 30px;
  margin-bottom: 30px;
  display: flex;
  justify-content: flex-end;
  align-items: center;
  gap: 10px;

  button {
    height: 100%;
    padding: 0 8px;
    font-size: 16px;
    border: none;
    background-color: $color-light;
    display: flex;
    justify-content: center;
    align-items: center;
    cursor: pointer;

    .fa-chevron-left,
    .fa-chevron-right {
      transform: translateY(1px);
    }

    .fa-chevron-left {
      margin-right: 10px;
    }

    .fa-chevron-right {
      margin-left: 10px;
    }
  }

  button:hover {
    background-color: $color-primary;
  }
}
</style>