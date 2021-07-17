<template>
  <li class="starship-item">
    <router-link :to="{ name: 'Detail', params: { id: starship.url.split('starships/')[1].slice(0, -1) }}">
      <img
        src="../assets/starship.svg"
        alt="Spaceship"
      >
      <h3>{{ starship.name }}</h3>
      <p class="model">
        <span>Model</span>: {{ starship.model }}
      </p>
      <p class="hyperdrive-rating"><span>Hyperdrive Rating</span>: {{ starship.hyperdrive_rating }}</p>
    </router-link>
  </li>
</template>

<script>
export default {
  name: "StarshipItem",
  props: {
    starship: {
      type: Object,
      required: true,
    },
  },
};
</script>

<style lang="scss" scoped>
// Imports
@import "../style/variables";

.starship-item {
  padding: 8px;
  background-image: url("../assets/starship-item-bg.jpg");
  background-size: cover;
  background-position: center;
  background-repeat: no-repeat;
  background-attachment: scroll;

  a {
    width: 100%;
    height: 100%;
    padding: 8px;
    background-color: rgba(#000, 0.8);
    border-top: 4px solid $color-secondary;
    border-bottom: 4px solid $color-tertiary;
    display: flex;
    flex-direction: column;
    align-items: center;

    img {
      width: 100%;
      margin-bottom: 16px;
    }

    h3 {
      width: 100%;
      padding: 4px;
      text-align: center;
      background-color: rgba($color-primary, 0.3);
      color: $color-light;
      font-size: 18px;
      margin-bottom: 8px;
    }

    p {
      width: 100%;
      margin-bottom: 8px;
      text-align: left;
      color: $color-light;

      span {
        color: $color-primary;
      }
    }
  }
}

// Media Queries
@media (max-width: 768px) {
  .starship-item {
    height: 50vw;
  }
}
</style>