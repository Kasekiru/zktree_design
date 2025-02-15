<template>
  <main role="main" class="container">
    <div style="padding-top: 7rem" class="d-none d-lg-block"></div>
    <div class="row justify-content-md-center">
      <div class="col-lg-4">
        <div class="text-center vstack gap-3">
          <h1>Your commitment</h1>
          <img :src="qrcodeDataUrl" />
          <div v-if="commitment" v-html="splitTwoLines(commitment.commitment)"></div>
          <button class="btn btn-info" @click="redirectToFlask">
            Register to Vote
          </button>
          <button class="btn btn-danger" @click="resetCommitment">
            Reset commitment
          </button>
          <a href="#/" class="btn btn-primary">Back</a>
        </div>
      </div>
    </div>
  </main>
</template>

<script>
import { ref, onMounted } from "vue";
import { generateCommitment } from "zk-merkle-tree";
import QRCode from "qrcode";

export default {
  setup() {
    const commitment = ref(null);
    const qrcodeDataUrl = ref("");
    const uniqueHash = "12"; // Unique hash statis

    const redirectToFlask = () => {
      const commitmentValue = commitment.value.commitment;
      if (commitmentValue) {
        window.location.href = `http://localhost:1234/#/validator?commitment=${commitmentValue}&uniqueHash=${uniqueHash}`;
      } else {
        alert("Commitment not found!");
      }
    };

    const init = async () => {
      commitment.value = JSON.parse(localStorage.getItem("zktree-vote-commitment"));
      if (!commitment.value) {
        commitment.value = await generateCommitment();
        localStorage.setItem("zktree-vote-commitment", JSON.stringify(commitment.value));
      }
      qrcodeDataUrl.value = await QRCode.toDataURL(commitment.value.commitment);
    };

    onMounted(init);

    const splitTwoLines = (text) => {
      const half = text.length / 2;
      return (
        text.substring(0, half) + "<br/>" + text.substring(half + 1, text.length)
      );
    };

    const resetCommitment = () => {
      localStorage.removeItem("zktree-vote-commitment");
      init();
    };

    return {
      commitment,
      qrcodeDataUrl,
      splitTwoLines,
      resetCommitment,
      redirectToFlask
    };
  },
};
</script>
