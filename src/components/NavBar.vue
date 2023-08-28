<template>
  <div class="nav">
    <routerLink to="/" class="logo_url">
      <img :src="logo" :alt="alt" class="logo" />
    </routerLink>
    <nav>
      <RouterLink to="/">Home</RouterLink> |
      <RouterLink to="/pedidos">Pedidos</RouterLink>
    </nav>
  </div>
</template>

<script>
export default {
  name: "NavBar",
  props: ["logo", "alt"],
};
</script>

<style scoped>
.nav {
  background-color: #222;
  border-bottom: 4px solid #111;
  padding: 15px 50px;
  display: flex;
  justify-content: space-between;
  align-items: center;
}

.logo_url {
  margin: auto;
  margin-left: 0;
}

.logo {
  width: 40px;
  height: 40px;
}

nav a {
      margin: 12px;
      transition: .5s;
      font-size: 20px;
}

nav a:hover {
      color: #fff;
} 

.nav a {
  color: #fcba03;
  text-decoration: none;
}
</style>
