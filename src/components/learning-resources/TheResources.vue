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
import StoredResources from './StoredResources.vue';
import AddResource from './AddResource.vue';

export default {
  components: {
    AddResource,
    StoredResources,
  },
  data() {
    return {
      selectedTab: 'stored-resources',
      storeResources: [
        {
          id: 'offical guide',
          title: 'Official Guide',
          description: 'The official Vue.js documentation.',
          link: 'https://vuejs.org',
        },
        {
          id: 'google',
          title: 'Google Guide',
          description: 'Learning everything',
          link: 'https://google.com',
        },
      ],
    };
  },
  provide() {
    return {
      resources: this.storeResources,
      addResource: this.addResource,
      deleteResource: this.removeResource,
    };
  },
  computed: {
    storedResButtonMode() {
      return this.selectedTab === 'stored-resources' ? null : 'flat';
    },
    addResButtonMode() {
      return this.selectedTab === 'add-resource' ? null : 'flat';
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
      this.storeResources.unshift(newResource);
      this.selectedTab = 'stored-resources';
    },
    removeResource(resId) {
      // this.storeResources = this.storeResources.filter((x) => x.id !== resId); // diffent array by copy
      const index = this.storeResources.findIndex((x) => x.id === resId);
      this.storeResources.splice(index, 1);
    },
  },
};
</script>
