<template>
  <div
    v-if="pagination"
    class="pagination"
  >
    <button
      v-if="pagination.previous"
      @click="$emit('get-page', pagination.previous)"
    ><i class="fas fa-chevron-left"></i></button>
    <button
      v-if="pagination.next"
      @click="$emit('get-page', pagination.next)"
    ><i class="fas fa-chevron-right"></i></button>
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
  margin-bottom: 20px;
  display: flex;
  justify-content: flex-end;
  align-items: center;
  gap: 10px;

  button {
    height: 100%;
    width: 30px;
    border: none;
    background-color: $color-light;
    border-radius: 6px;
    display: flex;
    justify-content: center;
    align-items: center;
    cursor: pointer;
  }

  button:hover {
    background-color: $color-primary;
  }
}
</style>