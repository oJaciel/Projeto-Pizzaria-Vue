<template>
  <div id="nav">
    <router-link to="/" id="img">
      <img :src="logo" :alt="alt" />
    </router-link>
    <div>
      <router-link to="/" class="nav-link">Home</router-link> |
      <router-link to="/pedidos" class="nav-link">Pedidos</router-link>
    </div>
  </div>
</template>

<script>
export default {
  name: "Navbar",
  props: ["logo", "alt"],
};
</script>

<style scoped>
#nav {
  background-color: #2c3e50;
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 20px 60px;
}

#img img {
  height: 40px;
}

.nav-link {
  color: gold;
  text-decoration: none;
  text-align: right;
}
</style>
