<template>
  <div class="form-page">
    <header class="form-header">Pendaftaran Kandidat</header>
    <div class="form-content">
      <h1>Isi data diri kamu</h1>
      <p class="sub-text">Pastikan sesuai dengan ID</p>
      <hr class="divider" />

      <form @submit.prevent="submitForm" class="form">
        <div class="form-group">
          <label for="id">Nomor ID</label>
          <input type="text" id="id" v-model="formData.id" />
        </div>
        <div class="form-group">
          <label for="name">Nama</label>
          <input type="text" id="name" v-model="formData.name" />
        </div>
        <div class="form-group">
          <label for="other">Data diri lainnya</label>
          <input type="text" id="other" v-model="formData.other" />
        </div>

        <!-- Input Upload Gambar -->
        <div class="form-group">
          <label for="image">Upload Foto Kandidat</label>
          <input type="file" id="image" @change="onFileChange" />
        </div>

        <!-- Tampilkan Gambar Setelah Diupload -->
        <img v-if="formData.imageUrl" :src="formData.imageUrl" alt="Foto Kandidat" class="preview-img" />

        <button type="submit" class="submit-btn">Daftar</button>
      </form>
    </div>
  </div>
</template>

<script>
import axios from "axios";

export default {
  data() {
    return {
      formData: {
        id: "",
        name: "",
        other: "",
        imageUrl: "", // Untuk menyimpan URL gambar yang diunggah
      },
      imageFile: null,
    };
  },
  methods: {
    onFileChange(event) {
      this.imageFile = event.target.files[0]; // Simpan file gambar yang dipilih
    },
    async submitForm() {
      if (!this.imageFile) {
        alert("Silakan pilih gambar terlebih dahulu.");
        return;
      }

      const formData = new FormData();
      formData.append("image", this.imageFile);

      try {
        // Upload gambar ke backend
        const res = await axios.post("http://localhost:5000/upload", formData, {
          headers: { "Content-Type": "multipart/form-data" },
        });

        // Simpan URL gambar yang diterima dari backend
        // this.formData.imageUrl = `http://localhost:5000${res.data.imageUrl}`;
        this.formData.imageUrl = res.data.imageUrl; // Pastikan langsung pakai URL yang diberikan backend

        alert("Gambar berhasil diunggah!");
      } catch (err) {
        console.error("Upload error:", err);
        alert("Gagal mengunggah gambar.");
      }
    },
  },
};
</script>

<style scoped>
/* Tambahkan style untuk preview gambar */
.preview-img {
  width: 150px;
  height: 150px;
  object-fit: cover;
  margin-top: 10px;
  border-radius: 10px;
  border: 1px solid #ccc;
}
</style>

<style scoped>
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
  font-family: Arial, sans-serif;
}

.form-page {
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  height: 100vh;
  width: 100vw;
  background: white;
}

.form-header {
  font-size: 2rem;
  /* font-weight: bold; */
  text-align: center;
  background: #d3d3d3;
  height: 15%;
  position: absolute;
  top: 0;
  width: 100%;
  padding: 20px 0;
  color: gray;
}

.form-content {
  text-align: center;
  width: 100%;
  max-width: 80%;
}

.sub-text {
  font-size: 1rem;
  /* color: gray; */
}

.divider {
  width: 80%;
  height: 1px;
  /* background: gray; */
  margin: 15px auto;
}

.form {
  width: 100%;
}

.form-group {
  display: flex;
  justify-content: space-between;
  align-items: center;
  margin-bottom: 15px;
  font-size: 1.2rem;
  width: 50%; /* ubah disini tinggal hapus aja biar cantik */
  margin-left: 50px; /* ubah disini tinggal hapus aja biar cantik */
}

.form-group label {
  flex: 1;
  text-align: left;
  /* font-weight: bold; */
}

.form-group input {
  flex: 2;
  padding: 10px;
  border: 1px solid #ccc;
  border-radius: 5px;
  font-size: 1rem;
  background: #d3d3d3;
}

.submit-btn {
  display: block;
  width: 20%;
  padding: 12px;
  font-size: 1.1rem;
  /* font-weight: bold; */
  background: #ccc;
  border: none;
  border-radius: 20px;
  cursor: pointer;
  transition: background 0.2s;
  margin: 30px auto 0;
}

.submit-btn:hover {
  background: #b0b0b0;
}

h1 {
  background-color: transparent;
  font-size: 2rem;
}
</style>
