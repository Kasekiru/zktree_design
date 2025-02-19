<template>
  <div class="container">
    <div class="left-section">
      <h1>Selamat datang <br />di pemilihan!</h1>
    </div>
    <div class="right-section">
      <div class="card">
        <ul class="options">
          <li><a href="/#/candidate">Pendaftaran Kandidat</a></li>
          <li><a href="/#/registration">Pendaftaran Pemilih</a></li>
          <li><a href="/#/vote">Pemberian Suara</a></li>
          <li><a href="/#/results">Hasil Pemilihan</a></li>
        </ul>
      </div>
    </div>
    <div class="help-button" @click="goToHelp">
      ?
    </div>
  </div>
</template>

<script>
export default {
  name: "Home",
  methods: {
    goToHelp() {
      window.location.href = "/#/guide"; // Ganti dengan route halaman panduan voting
    },
  },
};
</script>

<style scoped>
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
  font-family: Arial, sans-serif;
}

body, html {
  height: 100%;
  margin: 0;
}

.container {
  display: flex;
  height: 100vh; /* Full layar */
  width: 100vw;
}

.left-section {
  background-color: #b0b0b0;
  flex: 1;
  display: flex;
  align-items: center;
  justify-content: center;
  font-size: 2.5rem; /* Lebih besar agar lebih gagah */
  font-weight: bold;
}

.right-section {
  flex: 1;
  display: flex;
  align-items: center;
  justify-content: center;
}

.card {
  background: #d6d3d3;
  padding: 30px; /* Lebih besar */
  border-radius: 5px;
  box-shadow: 5px 5px 15px rgba(0, 0, 0, 0.2);
  width: 480px; /* Card lebih besar */
  text-align: center;
  margin-left: 200px;
}

.options {
  list-style: none;
  padding: 0;
}

.options li {
  margin: 20px 0;
}

.options li a {
  display: block;
  text-decoration: none;
  background: white;
  padding: 20px 30px; /* Lebih besar */
  border-radius: 5px;
  box-shadow: 4px 4px 12px rgba(0, 0, 0, 0.2);
  font-size: 1.2rem; /* Lebih besar */
  font-weight: bold;
  color: #303030;
  transition: transform 0.2s, box-shadow 0.2s;
  text-align: center;
}

.options li a:hover {
  transform: scale(1.08);
  box-shadow: 6px 6px 18px rgba(0, 0, 0, 0.3);
}

.help-button {
  position: fixed;
  bottom: 20px;
  right: 20px;
  width: 50px;
  height: 50px;
  background-color: #f39c12;
  color: white;
  font-size: 1.5rem;
  font-weight: bold;
  border-radius: 50%;
  display: flex;
  align-items: center;
  justify-content: center;
  cursor: pointer;
  box-shadow: 4px 4px 12px rgba(0, 0, 0, 0.3);
  transition: transform 0.2s, box-shadow 0.2s;
}

.help-button:hover {
  transform: scale(1.1);
  box-shadow: 6px 6px 18px rgba(0, 0, 0, 0.4);
}

</style>
