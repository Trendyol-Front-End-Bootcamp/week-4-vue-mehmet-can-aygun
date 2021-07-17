<template>
  <TheNavbar />
  <router-view />
</template>

<script>
import TheNavbar from "./components/TheNavbar";

export default {
  name: "App",
  components: {
    TheNavbar,
  },
};
</script>

<style lang="scss">
// Imports
@import "./style/variables";

// Reset
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
  font-family: "Segoe UI", Tahoma, Geneva, Verdana, sans-serif;
}

ul {
  list-style-type: none;
}

a {
  text-decoration: none;
}

body {
  background-color: #000;
  color: $color-light;
}
</style>
