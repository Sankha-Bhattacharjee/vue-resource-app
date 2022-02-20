<template>
  <base-card>
    <base-button
      @click="setSelectedTab('stored-resources')"
      :mode="storedResButtonMode"
      >Stored Resources</base-button
    >
    <base-button
      @click="setSelectedTab('add-resources')"
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
import AddResources from './AddResources.vue';
export default {
  components: {
    StoredResources,
    AddResources,
  },
  data() {
    return {
      selectedTab: 'stored-resources',
      storedResources: [
        {
          id: 'official-guide',
          title: 'Officoal Guide',
          description: 'Official Vue.js documntation.',
          link: 'https://vue.org',
        },
        {
          id: 'google',
          title: 'Google',
          description: 'Google search learning.',
          link: 'https://google.com',
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
      return this.selectedTab === 'stored-resources' ? null : 'flat';
    },
    addResButtonMode() {
      return this.selectedTab === 'add-resources' ? null : 'flat';
    },
  },
  methods: {
    setSelectedTab(tab) {
      this.selectedTab = tab;
    },
    addResource(title,desc,url){
      const newResource = {
        id: new Date().toISOString,
        title:title,
        description:desc,
        link:url
      };
      this.storedResources.unshift(newResource);
      this.selectedTab='stored-resources';
    },
    removeResource(id){
      const resIndex = this.storedResources.findIndex(res => res.id===id);
      console.log(resIndex);
      this.storedResources.splice(resIndex,1);
      
    },
  },
};
</script>
