<template>
  <div>
    <Navbar :logo="logo_src" :alt="app_name" />
    <router-view></router-view>
    <Footer />
  </div>
</template>

  <script>
import Navbar from "./components/Navbar.vue"
import Footer from "./components/Footer.vue"
export default {
  components: {
    Navbar,
    Footer,
  },
  data() {
    return {
      logo_src: "/img/logo.png",
      app_name: "Pizzaria"
    }
  }
};
</script>
  


<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}

body {
  margin: 0;
}
</style>
