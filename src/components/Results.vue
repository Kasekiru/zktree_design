<template>
  <header class="form-header">Hasil Pemilihan</header>
  <main role="main" class="container">
    <div style="padding-top: 10rem" class="d-none d-lg-block"></div>
    <div class="row justify-content-md-center">
      <div class="col-lg-6">
        <div class="text-center vstack gap-3">
          <!-- Gambar hidden untuk update URL masing-masing kandidat -->
          
          <!-- <img id="hiddenImage1" src="./../../public/encoded_image_1.png" style="display: none;" @load="updateImageUrl1">
          <img id="hiddenImage2" src="./../../public/encoded_image_2.png" style="display: none;" @load="updateImageUrl2">
          <img id="hiddenImage3" src="./../../public/encoded_image_3.png" style="display: none;" @load="updateImageUrl3">
          <img id="hiddenImage4" src="./../../public/encoded_image_4.png" style="display: none;" @load="updateImageUrl4">
          <img id="hiddenImage5" src="./../../public/encoded_image_5.png" style="display: none;" @load="updateImageUrl5"> -->

          <div class="table-container" v-if="!winner">
            <table class="custom-table">
              <thead>
                <tr>
                  <th>Foto Kandidat</th>
                  <th>Nama Kandidat</th>
                  <th>Jumlah Suara</th>
                </tr>
              </thead>
              <tbody>
                <tr v-for="(candidate, index) in candidates" :key="index">
                  <td><img :src="candidate.photo" alt="Foto Kandidat" class="candidate-photo"></td>
                  <td>{{ candidate.name }}</td>
                  <td>{{ candidate.votes }}</td>
                </tr>
              </tbody>
            </table>
          </div>

          <div class="table-container" v-if="winner">
            <table class="custom-table">
              <thead>
                <tr>
                  <th>Foto Kandidat</th>
                  <th>Nama Kandidat</th>
                  <th>Jumlah Suara</th>
                </tr>
              </thead>
              <tbody>
                <tr>
                  <td><img :src="winner.photo" alt="Foto Pemenang" class="candidate-photo"></td>
                  <td>{{ winner.name }}</td>
                  <td>{{ winner.votes }}</td>
                </tr>
              </tbody>
            </table>
          </div>

          <button v-if="!winner" @click="announceWinner" class="btn btn-primary">Umumkan Pemenang</button>
        </div>
      </div>
    </div>
  </main>
</template>

<script>
import { ref, onMounted } from "vue";
import * as ethers from "ethers";

export default {
  setup() {
    // const candidates = ref([
    //   { id: "017815", name: "Jonatan", votes: 0, photo: "/encoded_image_1.png" },
    //   { id: "018435", name: "Kennedy", votes: 0, photo: "/encoded_image_2.png" },
    //   { id: "019482", name: "Sonata", votes: 0, photo: "/encoded_image_3.png" },
    //   { id: "020985", name: "Michael", votes: 0, photo: "/encoded_image_4.png" },
    //   { id: "028208", name: "Enellys", votes: 0, photo: "/encoded_image_5.png" }
    // ]);
    const candidates = ref([
      { id: "017815", name: "Jonatan", votes: 0, photo: new URL('../assets/encoded_image_1.png', import.meta.url).href },
      { id: "018435", name: "Kennedy", votes: 0, photo: new URL('../assets/encoded_image_2.png', import.meta.url).href },
      { id: "019482", name: "Sonata", votes: 0, photo: new URL('../assets/encoded_image_3.png', import.meta.url).href },
      { id: "020985", name: "Michael", votes: 0, photo: new URL('../assets/encoded_image_4.png', import.meta.url).href },
      { id: "028208", name: "Enellys", votes: 0, photo: new URL('../assets/encoded_image_5.png', import.meta.url).href }
    ]);

    const winner = ref(null);

    // Fungsi untuk update gambar kandidat masing-masing
    const updateImageUrl1 = () => {
      const hiddenImg = document.getElementById("hiddenImage1");
      if (hiddenImg) {
        candidates.value[0].photo = hiddenImg.src + "?" + new Date().getTime();
      }
    };

    const updateImageUrl2 = () => {
      const hiddenImg = document.getElementById("hiddenImage2");
      if (hiddenImg) {
        candidates.value[1].photo = hiddenImg.src + "?" + new Date().getTime();
      }
    };

    const updateImageUrl3 = () => {
      const hiddenImg = document.getElementById("hiddenImage3");
      if (hiddenImg) {
        candidates.value[2].photo = hiddenImg.src + "?" + new Date().getTime();
      }
    };

    const updateImageUrl4 = () => {
      const hiddenImg = document.getElementById("hiddenImage4");
      if (hiddenImg) {
        candidates.value[3].photo = hiddenImg.src + "?" + new Date().getTime();
      }
    };

    const updateImageUrl5 = () => {
      const hiddenImg = document.getElementById("hiddenImage5");
      if (hiddenImg) {
        candidates.value[4].photo = hiddenImg.src + "?" + new Date().getTime();
      }
    };

    const init = async () => {
      const abi = ["function getOptionCounter(uint _option) external view returns (uint)"];
      const provider = new ethers.providers.Web3Provider(window.ethereum);
      const signer = provider.getSigner();
      const contracts = await (await fetch("contracts.json")).json();
      const contract = new ethers.Contract(contracts.zktreevote, abi, signer);

      for (let i = 0; i < candidates.value.length; i++) {
        const count = await contract.getOptionCounter(i + 1);
        candidates.value[i].votes = parseInt(count.toString());
      }
    };

    const announceWinner = () => {
      winner.value = candidates.value.reduce((max, candidate) =>
        candidate.votes > max.votes ? candidate : max, candidates.value[0]
      );
    };

    onMounted(() => {
      init();
    });

    return {
      candidates,
      winner,
      announceWinner,
      updateImageUrl1,
      updateImageUrl2,
      updateImageUrl3,
      updateImageUrl4,
      updateImageUrl5
    };
  }
};
</script>

<style scoped>
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

.table-container {
  display: flex;
  justify-content: center;
}

.custom-table {
  width: 100%;
  border-collapse: separate;
  border-spacing: 0;
  border: 2px solid black;
  border-radius: 10px;
  overflow: hidden;
  text-align: center;
}

.custom-table th {
  background: white;
  border-bottom: 2px solid black;
  padding: 8px;
}

.custom-table td {
  padding: 10px;
  border-bottom: 2px solid black;
}

.custom-table tr:last-child td {
  border-bottom: none;
}

.candidate-photo {
  width: 50px;
  height: 50px;
  border-radius: 50%;
}
</style>
