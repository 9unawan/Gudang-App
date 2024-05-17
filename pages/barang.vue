<template>
  <div class="container">
    <h1 class="title">Data Barang</h1>
    <ul class="item-list">
      <li v-for="item in barang" :key="item.barangId" class="item">
        <span
          >{{ item.nama_barang }} - {{ item.harga }} - {{ item.jumlah }}</span
        >
        <button
          @click="deleteBarang(item.kategoriId, item.barangId)"
          class="delete-btn"
        >
          Delete
        </button>
      </li>
    </ul>
    <form @submit.prevent="addBarang" class="form">
      <input
        v-model="newBarang.nama_barang"
        placeholder="Nama Barang"
        required
      />
      <input
        v-model="newBarang.harga"
        type="number"
        placeholder="Harga Barang"
        required
      />
      <input
        v-model="newBarang.jumlah"
        type="number"
        placeholder="Jumlah Barang"
        required
      />
      <input
        v-model="newBarang.kategoriId"
        type="number"
        placeholder="Kategori ID"
        required
      />
      <button type="submit" class="submit-btn">Tambah Barang</button>
    </form>
  </div>
</template>

<script>
export default {
  data() {
    return {
      barang: [],
      newBarang: {
        nama_barang: "",
        harga: "",
        jumlah: "",
        kategoriId: "",
      },
    };
  },
  async mounted() {
    const response = await this.$axios.$get("barang");
    this.barang = response;
  },
  methods: {
    async addBarang() {
      const response = await this.$axios.$post(
        `kategori/${this.newBarang.kategoriId}/barang`,
        this.newBarang
      );
      this.barang.push(response);
      this.newBarang = {
        nama_barang: "",
        harga: "",
        jumlah: "",
        kategoriId: "",
      };
    },
    async deleteBarang(kategoriId, barangId) {
      await this.$axios.$delete(`kategori/${kategoriId}/barang/${barangId}`);
      this.barang = this.barang.filter((item) => item.barangId !== barangId);
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
