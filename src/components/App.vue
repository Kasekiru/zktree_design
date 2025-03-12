<template>
  <component :is="getMainComponent()"></component>
</template>

<script>
import { ref, onMounted } from "vue";
import Home from "./Home.vue";
import ValidatorTool from "./ValidatorTool.vue";
import VoterRegistration from "./VoterRegistration.vue";
import CandidateRegistration from "./CandidateRegistration.vue";
import Vote from "./Vote.vue";
import Results from "./Results.vue";

export default {
  setup() {
    const locationHash = ref(window.location.hash);

    // Update locationHash when the hash changes
    const updateLocationHash = () => {
      locationHash.value = window.location.hash;
    };

    onMounted(() => {
      window.addEventListener("hashchange", updateLocationHash);
    });

    // Get the main component based on the current location hash
    const getMainComponent = () => {
      // const currentPath = locationHash.value.slice(1) || "/";
      const currentPath = locationHash.value.slice(1).split('?')[0] || "/";
      if (currentPath === "/") return Home;
      if (currentPath === "/registration") return VoterRegistration;
      if (currentPath === "/candidate") return CandidateRegistration;
      if (currentPath === "/vote") return Vote;
      if (currentPath === "/results") return Results;
      if (currentPath === "/validator") return ValidatorTool;
    };

    return {
      getMainComponent,
    };
  },
};
</script>
