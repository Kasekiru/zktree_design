<template>
  <div class="fullscreen">
    <header class="form-header">Pemberian Suara</header>
    <div v-if="!showResults" class="form-container">
      <div v-if="showForm" class="flex-container">
        <div class="container-input">
          <div class="form-group">
            <label>Commitment:</label>
            <input type="text" v-model="commitment" class="styled-input" />
          </div>
          <div class="form-group">
            <label>Secret:</label>
            <input type="text" v-model="secret" class="styled-input" />
          </div>
          <div class="form-group">
            <label>Nullifier:</label>
            <input type="text" v-model="nullifier" class="styled-input" />
          </div>
        </div>
        <div class="upload-section">
          <span>Atau unggah file bukti untuk pengisian otomatis</span>
          <button class="upload-button">Unggah file bukti</button>
        </div>
      </div>
      <button v-if="showForm" class="next-button" @click="showResults = true">Selanjutnya</button>
      <button v-else class="connect-button" @click="showForm = true">Hubungkan wallet Metamask</button>
    </div>
    <div v-else>
      <main role="main" class="container">
        <div style="padding-top: 5rem" class="d-none d-lg-block"></div>
        <div style="width: 900px;" class="row justify-content-md-center">
          <div class="col-lg-6">
            <div class="text-center vstack gap-3">
              <div class="table-container">
                <table class="custom-table">
                  <thead>
                    <tr>
                      <th>No ID Kandidat</th>
                      <th>Nama Kandidat</th>
                      <th>Aksi</th>
                    </tr>
                  </thead>
                  <tbody>
                    <tr v-for="(candidate, index) in candidates" :key="index">
                      <td>{{ candidate.id }}</td>
                      <td>{{ candidate.name }}</td>
                      <td>
                        <button class="vote-button" @click="vote(candidate.id)">Pilih</button>
                      </td>
                    </tr>
                  </tbody>
                </table>
              </div>
              <!-- <button class="btn btn-primary" @click="showResults = false">Kembali</button> -->
            </div>
          </div>
        </div>
      </main>
    </div>
  </div>
</template>

<script>
import { ref } from "vue";

export default {
  setup() {
    const showForm = ref(false);
    const showResults = ref(false);
    const commitment = ref("");
    const secret = ref("");
    const nullifier = ref("");
    const candidates = ref([
      { id: "017815", name: "Jonatan" },
      { id: "018435", name: "Kennedy" },
      { id: "019482", name: "Sonata" },
      { id: "020985", name: "Michael" },
      { id: "028208", name: "Enellys" },
    ]);

    const vote = (id) => {
      alert(`Anda memilih kandidat dengan ID: ${id}`);
    };

    return { showForm, showResults, commitment, secret, nullifier, candidates, vote };
  }
};
</script>

<style>
.fullscreen {
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  height: 100vh;
  background: white;
}

.form-header {
  font-size: 2rem;
  text-align: center;
  background: #d3d3d3;
  height: 15%;
  position: absolute;
  top: 0;
  width: 100%;
  padding: 20px 0;
  color: gray;
}

.flex-container {
  display: flex;
  justify-content: space-between;
  align-items: flex-start;
  width: 100%;
  max-width: 900px;
}

.container-input {
  flex: 1;
}

.form-group {
  display: flex;
  align-items: center;
  justify-content: space-between;
  width: 100%;
  margin-bottom: 10px;
}

.form-group label {
  width: 120px;
  text-align: left;
}

.styled-input {
  flex: 1;
  padding: 10px;
  border: 1px solid #ccc;
  border-radius: 5px;
  height: 30px;
  background: #e0e0e0;
}

.upload-section {
  display: flex;
  flex-direction: column;
  align-items: flex-start;
  margin-left: 20px;
}

.upload-button, .next-button, .vote-button {
  padding: 8px 12px;
  background: #d3d3d3;
  border: none;
  cursor: pointer;
  border-radius: 5px;
}

.vote-button {
  background: #4caf50;
  color: white;
}

.fullscreen {
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  height: 100vh;
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

.form-group {
  display: flex;
  align-items: center;
  justify-content: space-between;
  width: 100%;
  margin-bottom: 10px;
}

.form-group label {
  width: 120px;
  text-align: left;
}

.styled-input {
  flex: 1;
  padding: 10px;
  border: 1px solid #ccc;
  border-radius: 5px;
  height: 30px;
  background: #e0e0e0;
}

.upload-section {
  display: flex;
  flex-direction: column;
  align-items: flex-start;
  margin-left: 20px;
}

.upload-button {
  padding: 6px 12px;
  background: #d3d3d3;
  border: none;
  cursor: pointer;
  border-radius: 5px;
}

.form-container {
  display: flex;
  flex-direction: column;
  align-items: center;
  width: 100%;
  max-width: 600px;
  margin-bottom: 10%;
}

.next-button {
  margin-top: 20px;
  padding: 8px 15px;
  background: #d3d3d3;
  border: none;
  cursor: pointer;
  border-radius: 5px;
}

.connect-button {
  margin-bottom: 20%;
  padding: 3px;
  background: lightgray;
  border: none;
  cursor: pointer;
  width: 50%;
  text-align: center;
}

/* Atur kontainer tabel */
.table-container {
  display: flex;
  justify-content: center;
  width: 100%;
}

/* Tabel dengan desain membulat dan border hitam */
.custom-table {
  width: 100%;
  max-width: 900px;
  border-collapse: separate;
  border-spacing: 0;
  border: 2px solid black;
  border-radius: 10px;
  overflow: hidden;
  text-align: center;
  margin-bottom: 10%;
}

/* Header tabel */
.custom-table th {
  background: white;
  border-bottom: 2px solid black;
  padding: 12px;
  font-weight: bold;
}

/* Sel tabel */
.custom-table td {
  padding: 14px;
  border-bottom: 2px solid black;
}

/* Hilangkan border bawah untuk baris terakhir */
.custom-table tr:last-child td {
  border-bottom: none;
}

/* Styling tombol "Pilih" agar kecil dan abu-abu */
.vote-button {
  padding: 5px 15px;
  background: #d3d3d3;
  border: none;
  cursor: pointer;
  border-radius: 5px;
  font-size: 14px;
  color: gray;
}

/* Agar tombol berada di tengah */
.custom-table td:last-child {
  text-align: center;
}

.vote-button:hover {
  background: #595959;
  color:#d3d3d3
}

</style>
