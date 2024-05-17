<template>
  <div class="container">
    <h1 class="title">Data Kategori</h1>
    <ul class="item-list">
      <li v-for="item in kategori" :key="item.kategoriId" class="item">
        <span>{{ item.kategori }} - {{ item.keterangan }}</span>
        <button @click="deleteKategori(item.kategoriId)" class="delete-btn">
          Delete
        </button>
      </li>
    </ul>
    <form @submit.prevent="addKategori" class="form">
      <input
        v-model="newKategori.kategori"
        placeholder="Nama Kategori"
        required
      />
      <input
        v-model="newKategori.keterangan"
        placeholder="Keterangan"
        required
      />
      <button type="submit" class="submit-btn">Tambah Kategori</button>
    </form>
  </div>
</template>

<script>
export default {
  data() {
    return {
      kategori: [],
      newKategori: {
        kategori: "",
        keterangan: "",
      },
    };
  },
  async mounted() {
    const response = await this.$axios.$get("kategori");
    this.kategori = response;
  },
  methods: {
    async addKategori() {
      const response = await this.$axios.$post("kategori", this.newKategori);
      this.kategori.push(response);
      this.newKategori = { kategori: "", keterangan: "" };
    },
    async deleteKategori(kategoriId) {
      await this.$axios.$delete(`kategori/${kategoriId}`);
      this.kategori = this.kategori.filter(
        (item) => item.kategoriId !== kategoriId
      );
    },
  },
};
</script>

<style scoped>
.container {
  padding: 20px;
}
.title {
  text-align: center;
  margin-bottom: 20px;
}
.item-list {
  list-style: none;
  padding: 0;
}
.item {
  display: flex;
  justify-content: space-between;
  padding: 10px;
  border-bottom: 1px solid #ccc;
}
.delete-btn {
  background-color: #dc3545;
  color: white;
  border: none;
  padding: 5px 10px;
  border-radius: 5px;
  cursor: pointer;
}
.delete-btn:hover {
  background-color: #c82333;
}
.form {
  display: flex;
  flex-direction: column;
  gap: 10px;
  margin-top: 20px;
}
.form input {
  padding: 10px;
  border: 1px solid #ccc;
  border-radius: 5px;
}
.submit-btn {
  padding: 10px;
  background-color: #28a745;
  color: white;
  border: none;
  border-radius: 5px;
  cursor: pointer;
}
.submit-btn:hover {
  background-color: #218838;
}
</style>
