<template>
  <div class="main-banner">
    <h1>Faça o seu Hambúrguer</h1>
  </div>
</template>

<script>
export default {
  name: "Banner",
};
</script>

<style scoped>
.main-banner {
  background-image: url("/img/burger.jpg");
  background-position: 0 -250px;
  background-size: cover;
  display: flex;
  align-items: center;
  justify-content: flex-start;
  width: 100%;
  height: 500px;
}

.main-banner h1 {
  color: #fff;
  text-align: center;
  font-size: 60px;
  background-color: #222;
  padding: 20px 40px;
  border-radius: 10px;
}
</style>
