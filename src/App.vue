<template>
  <Header />
  <router-view />
</template>

<script>
import Header from "./components/Header.vue"
export default {
  name: "App",
  components: {
    Header,
  },
}
</script>

<style>
@import url("https://fonts.googleapis.com/css2?family=Poppins:wght@300;400&display=swap");
#app {
  font-family: "Poppins", sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
}
</style>
