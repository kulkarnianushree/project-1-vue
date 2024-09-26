<template>
    <base-card>
      <base-button @click="setSelectedTab('StoredResources')" :mode="storedResButton">Stored Resources</base-button>
      <base-button @click="setSelectedTab('AddResources')" :mode="addResButton">Add Resources</base-button>
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
        selectedTab: 'StoredResources', 
        storedResource: [
          {
            id: '1',
            title: 'Official Guide',
            description: 'The Official vue.js documentation',
            link: 'https://vuejs.org',
          },
          {
            id: '2',
            title: 'Google',
            description: 'Learn to Google..!',
            link: 'https://google.com',
          },
        ],
      };
    },
    provide() {
      return {
        resources: this.storedResource,
        formSubmit:this.submitHandler,
        deleteResource:this.deleteHandler,
      };
    },
    computed:{
        storedResButton(){
            return this.selectedTab === 'StoredResources'? null :'flat'
        },
        addResButton(){
            return this.selectedTab === 'AddResource' ? null : 'flat'
        }
    },
    methods: {
      setSelectedTab(tab) {
        this.selectedTab = tab;
      },
      submitHandler(res){
        this.storedResource.push(res)
      },
      deleteHandler(idx){
        this.storedResource = this.storedResource.filter((resource)=>resource.id !== idx)
      }
    },
  };
  </script>
  