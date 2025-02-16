<template>
  <div class="fullscreen">
    <header class="form-header">Pemberian Suara</header>
    <div v-if="showForm" class="form-container">
      <div class="flex-container">
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
      <button class="next-button">Selanjutnya</button>
    </div>
    <button v-else class="connect-button" @click="showForm = true">Hubungkan wallet Metamask</button>
  </div>
</template>

<script>
export default {
  data() {
    return {
      showForm: false,
      commitment: '',
      secret: '',
      nullifier: ''
    };
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
  font-weight: bold;
  text-align: center;
  background: #d3d3d3;
  height: 15%;
  position: absolute;
  top: 0;
  width: 100%;
  padding: 20px 0;
}

.flex-container {
  display: flex;
  justify-content: space-between;
  align-items: flex-start;
  width: 100%;
  max-width: 600px;
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
  width: 20%;
  text-align: center;
}
</style>
