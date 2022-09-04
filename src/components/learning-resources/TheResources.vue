<template>
  <base-card>
    <base-button
      @click="setSelectedTab('stored-resources')"
      :mode="storedResButtonMode"
      >Stored Resources</base-button
    >
    <base-button
      @click="setSelectedTab('add-resource')"
      :mode="addResButtonMode"
      >Add Resource</base-button
    >
  </base-card>
  <keep-alive>
    <component :is="selectedTab"></component>
  </keep-alive>
</template>

<script>
import BaseButton from "@/components/UI/BaseButton.vue";
import BaseCard from "@/components/UI/BaseCard.vue";
import StoredResources from "@/components/learning-resources/StoredResources.vue";
import AddResource from "@/components/learning-resources/AddResource.vue";
export default {
  components: { BaseCard, BaseButton, StoredResources, AddResource },

  data() {
    return {
      selectedTab: "stored-resources",
      storedResources: [
        {
          id: 1,
          title: "Vue JS",
          description: "Qui minus nobis vitae.",
          link: "https://vuejs.org/",
        },
        {
          id: 2,
          title: "Google",
          description: "Itaque laudantium cum dolor consequatur..",
          link: "https://google.com/",
        },
      ],
    };
  },

  provide() {
    return {
      resources: this.storedResources,
      addResource: this.addResource,
      deleteResource: this.removeResource,
    };
  },

  computed: {
    storedResButtonMode() {
      return this.selectedTab === "stored-resources" ? null : "flat";
    },
    addResButtonMode() {
      return this.selectedTab === "add-resource" ? null : "flat";
    },
  },
  methods: {
    setSelectedTab(tab) {
      this.selectedTab = tab;
    },

    addResource(title, description, url) {
      const newResource = {
        id: new Date().toISOString(),
        title: title,
        description: description,
        link: url,
      };
      this.storedResources.unshift(newResource);
      this.selectedTab = "stored-resources";
    },

    removeResource(resId) {
      // eski yontem
      // this.storedResources = this.storedResources.filter(
      //   (res) => res.id !== resId
      // );
      //
      // console.log(this.storedResources.length);

      //  yeni

      const resIndex = this.storedResources.findIndex(
        (res) => res.id === resId
      );
      this.storedResources.splice(resIndex, 1);
    },
  },
};
</script>

<style scoped></style>
