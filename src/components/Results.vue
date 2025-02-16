<template>
  <header class="form-header">Hasil Pemilihan</header>
  <main role="main" class="container">
    <div style="padding-top: 10rem" class="d-none d-lg-block"></div>
    <div class="row justify-content-md-center">
      <div class="col-lg-6">
        <div class="text-center vstack gap-3">
          <div class="table-container">
            <table class="custom-table">
              <thead>
                <tr>
                  <th>No ID Kandidat</th>
                  <th>Nama Kandidat</th>
                  <th>Jumlah Suara</th>
                </tr>
              </thead>
              <tbody>
                <tr v-for="(candidate, index) in candidates" :key="index">
                  <td>{{ candidate.id }}</td>
                  <td>{{ candidate.name }}</td>
                  <td>{{ candidate.votes }}</td>
                </tr>
              </tbody>
            </table>
          </div>
          <a href="#/" class="btn btn-primary">Back</a>
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
    const candidates = ref([
      { id: "017815", name: "Jonatan", votes: 0 },
      { id: "018435", name: "Kennedy", votes: 0 },
      { id: "019482", name: "Sonata", votes: 0 },
      { id: "020985", name: "Michael", votes: 0 },
      { id: "028208", name: "Enellys", votes: 0 },
    ]);

    const init = async () => {
      const abi = ["function getOptionCounter(uint _option) external view returns (uint)"];
      const provider = new ethers.providers.Web3Provider(window.ethereum);
      const signer = provider.getSigner();
      const contracts = await (await fetch("contracts.json")).json();
      const contract = new ethers.Contract(contracts.zktreevote, abi, signer);

      for (let i = 0; i < candidates.value.length; i++) {
        const count = await contract.getOptionCounter(i + 1);
        candidates.value[i].votes = count.toString();
      }
    };

    onMounted(() => {
      init();
    });

    return { candidates };
  }
};
</script>

<style scoped>
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
</style>
