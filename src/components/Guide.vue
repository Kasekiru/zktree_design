<template>
  <div class="guide-container">
    <h1>Panduan Voting</h1>
    <div class="guide-content">
      <ol>
        <li>
          <strong> Pendaftaran:</strong>
          <p>Jika Anda ingin memilih, daftarkan diri di <a href="/#/registration">Pendaftaran Pemilih</a>. Jika ingin menjadi kandidat, daftar di <a href="/#/candidate">Pendaftaran Kandidat</a>.</p>
        </li>
        <li>
          <strong> Menunggu Proses Pendaftaran:</strong>
          <p>Setelah semua pendaftar masuk, halaman voting akan dibuka.</p>
        </li>
        <li>
          <strong> Menghubungkan Wallet:</strong>
          <p>Ketika halaman voting dibuka, hubungkan wallet MetaMask Anda.</p>
        </li>
        <li>
          <strong> Memasukkan Tiket:</strong>
          <p>Masukkan tiket yang Anda dapatkan saat mendaftar atau gunakan fitur scan QR untuk input otomatis.</p>
        </li>
        <li>
          <strong> Melakukan Voting:</strong>
          <p>Setelah tiket berhasil diverifikasi, Anda dapat memilih kandidat yang terdaftar.</p>
        </li>
        <li>
          <strong> Melihat Hasil:</strong>
          <p>Setelah voting selesai, Anda dapat melihat total suara di halaman <a href="/#/results">Hasil Pemilihan</a>.</p>
        </li>
      </ol>
    </div>
  </div>
</template>

<style scoped>
.guide-container {
  max-width: 800px;
  margin: 50px auto;
  padding: 20px;
  background: #f9f9f9;
  border-radius: 8px;
  box-shadow: 4px 4px 12px rgba(0, 0, 0, 0.1);
}

h1 {
  text-align: center;
  margin-bottom: 20px;
}

.guide-content {
  font-size: 1.1rem;
  line-height: 1.6;
}

ol {
  padding-left: 20px;
}

li {
  margin-bottom: 15px;
}

strong {
  color: #2c3e50;
}

p {
  margin: 5px 0;
}

a {
  color: #3498db;
  text-decoration: none;
}

a:hover {
  text-decoration: underline;
}
</style>
