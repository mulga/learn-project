<template>
  <the-header title="Study App"></the-header>
  <the-resources></the-resources>
</template>

<script>
import TheHeader from "@/components/layouts/TheHeader.vue";
import TheResources from "@/components/learning-resources/TheResources.vue";

// import LearningResources from "@/components/learning-resources/LearningResources.vue";
export default {
  name: "App",
  components: { TheResources, TheHeader },
};
</script>

<style></style>
