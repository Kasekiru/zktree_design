<template>
  <main role="main" class="container">
    <div style="padding-top: 7rem" class="d-none d-lg-block"></div>
    <div class="row justify-content-md-center">
      <div class="col-lg-4">
        <div class="text-center vstack gap-3">
          <h1>Results</h1>
          <div class="text-start">1st option: {{ options[0] }}</div>
          <div class="text-start">2nd option: {{ options[1] }}</div>
          <div class="text-start">3rd option: {{ options[2] }}</div>
          <div class="text-start">4th option: {{ options[3] }}</div>
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
    const options = ref([0, 0, 0, 0]);

    // Function to initialize the contract interaction
    const init = async () => {
      const abi = [
        "function getOptionCounter(uint _option) external view returns (uint)"
      ];
      const provider = new ethers.providers.Web3Provider(window.ethereum);
      const signer = provider.getSigner();
      const contracts = await (await fetch("contracts.json")).json();
      const contract = new ethers.Contract(contracts.zktreevote, abi, signer);

      // Fetch the option counts from the contract and update the options
      for (let i = 0; i < 4; i++) {
        const count = await contract.getOptionCounter(i + 1);
        options.value[i] = count.toString();
      }

      console.log(options.value[3]);
    };

    // Use the onMounted hook to call the init function after the component is mounted
    onMounted(() => {
      init();
    });

    return { options };
  }
};
</script>
