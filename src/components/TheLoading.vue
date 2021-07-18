<template>
  <div class="loading-container">
    <div class="loading"></div>
  </div>
</template>

<script>
export default {
  name: "TheLoading",
};
</script>

<style lang="scss" scoped>
// Imports
@import "../style/variables";

.loading-container {
  height: 230px;
  display: flex;
  justify-content: center;
  align-items: center;

  .loading {
    width: 200px;
    height: 200px;
    border-radius: 50%;
    border: 12px solid rgba($color-primary, 0.2);
    border-top: 12px solid $color-primary;
    animation: loading 0.5s ease-in-out infinite;
  }
}

@keyframes loading {
  from {
    transform: rotate(0deg);
  }
  to {
    transform: rotate(360deg);
  }
}

// Media Queries
@media (max-width: 768px) {
  .loading-container {
    height: 200px;

    .loading {
      width: 120px;
      height: 120px;
    }
  }
}
</style>