<template>
  <main role="main" class="container">
    <div style="padding-top: 7rem" class="d-none d-lg-block"></div>
    <div class="row justify-content-md-center">
      <div class="col-lg-4 text-center">
        <h1>Validator Tool</h1>
        <p v-if="loading">Processing transaction...</p>
        <p v-if="commitment && uniqueHash">Commitment: {{ commitment }}</p>
        <p v-if="commitment && uniqueHash">Unique Hash: {{ uniqueHash }}</p>
      </div>
    </div>
  </main>
</template>

<script>
import { ref, onMounted } from "vue";
import { ethers } from "ethers";

export default {
  setup() {
    const commitment = ref("");
    const uniqueHash = ref("");
    const loading = ref(true);

    // PRIVATE KEY HARDCODED (PASTIKAN PRIVATE KEY VALID!)
    const privateKey =
      "0x59c6995e998f97a5a0044966f0945389dc9e86dae88c7a8412f4603b6b78690d"; 

    // Fungsi ambil parameter dari URL (mendukung hash #)
    const getQueryParams = () => {
      let queryString = window.location.search; // Default: ambil dari search (?)
      
      if (!queryString) {
        // Jika kosong, coba ambil dari hash (#)
        const hashPart = window.location.hash.split("?");
        if (hashPart.length > 1) {
          queryString = "?" + hashPart[1]; // Format ulang biar bisa diproses URLSearchParams
        }
      }

      const params = new URLSearchParams(queryString);
      return {
        commitment: params.get("commitment"),
        uniqueHash: params.get("uniqueHash"),
      };
    };

    // Fungsi otomatis kirim transaksi
    const processTransaction = async (commitmentValue, uniqueHashValue) => {
      try {
        if (!commitmentValue || !uniqueHashValue) {
          alert("❌ Error: Commitment dan Unique Hash tidak ditemukan.");
          return;
        }

        console.log("🚀 Memulai transaksi...");

        const provider = new ethers.providers.JsonRpcProvider("http://127.0.0.1:8545/");
        const wallet = new ethers.Wallet(privateKey, provider);

        // ABI dari kontrak
        const abi = [
          "function registerCommitment(uint256 _uniqueHash, uint256 _commitment)"
        ];

        // Ambil alamat kontrak dari file JSON
        const contracts = await (await fetch("contracts.json")).json();
        console.log("📌 Contract Address:", contracts.zktreevote);

        const contract = new ethers.Contract(contracts.zktreevote, abi, wallet);
        const commitmentBigNumber = ethers.BigNumber.from(commitmentValue);
        const uniqueHashBigNumber = ethers.BigNumber.from(uniqueHashValue);

        // Kirim transaksi
        const tx = await contract.registerCommitment(uniqueHashBigNumber, commitmentBigNumber);
        console.log("✅ Transaksi berhasil! TX Hash:", tx.hash);

        alert(`✅ Transaction successful!\nTX Hash: ${tx.hash}\nYou can now vote.`);
      } catch (error) {
        console.error("❌ Blockchain Error:", error);
        alert(`❌ Error: ${error.reason || "Terjadi kesalahan."}`);
      } finally {
        loading.value = false;
      }
    };

    onMounted(async () => {
      // Ambil parameter dari URL
      const { commitment: commitmentValue, uniqueHash: uniqueHashValue } = getQueryParams();
      if (commitmentValue && uniqueHashValue) {
        commitment.value = commitmentValue;
        uniqueHash.value = uniqueHashValue;

        // Langsung jalankan transaksi
        await processTransaction(commitmentValue, uniqueHashValue);
      } else {
        alert("❌ Error: Parameter tidak lengkap di URL.");
        loading.value = false;
      }
    });

    return { commitment, uniqueHash, loading };
  },
};
</script>
