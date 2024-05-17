<template>
  <div class="container">
    <h1 class="title">Gudang App</h1>
    <div class="links">
      <nuxt-link to="/barang" class="link">Data Barang</nuxt-link>
      <nuxt-link to="/kategori" class="link">Data Kategori</nuxt-link>
    </div>
  </div>
</template>

<style scoped>
.container {
  text-align: center;
  margin-top: 50px;
}
.title {
  font-size: 2.5em;
  margin-bottom: 20px;
}
.links {
  display: flex;
  justify-content: center;
  gap: 20px;
}
.link {
  padding: 10px 20px;
  background-color: #00ff4c;
  color: rgb(255, 255, 255);
  border-radius: 5px;
  text-decoration: none;
}
.link:hover {
  background-color: #2d7a00;
}
</style>
