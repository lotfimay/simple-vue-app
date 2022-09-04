<template>
    <base-card>
        <base-button @click="setActiveTab('resource-list')" :mode="storedResourcesMode">Stored Resources</base-button>
        <base-button @click="setActiveTab('add-resource')" :mode="addResourcesMode">Add Resource</base-button>
    </base-card>
    <component :is="activeTab"></component>
    

</template>
<script>
import ResourceList from './ResourceList.vue';
import AddResource from './AddResource.vue'
export default {
    components : {
        ResourceList,
        AddResource,
    },
    data(){
      return {
        storedResources : [
        {id : 'vue-guide' , title : 'Official Guide' , description : 'Vue is Front-end framework' , link :'https://vuejs.org/'},
        {id : 'java-guide' , title : 'Official Guide' , description : 'Java id OOP language' , link :'https://vuejs.org/'}
        ],
        activeTab :  'resource-list'
      }
    },
    provide(){
        return {
            resources : this.storedResources,
            addResource : this.addResource,
            deleteResource : this.deleteResource,
            changeTab : this.changeTab 
        }
    },
    methods : {
        setActiveTab(tab){
            this.activeTab = tab;
        },
        addResource(data){
            this.storedResources.unshift(data);
        },
        deleteResource(resId){
            const index = this.storedResources.findIndex((resource) => resource.id === resId);
            this.storedResources.splice(index , 1);
        },
        changeTab(){
            this.activeTab = 'resource-list';
        }
    },
    computed : {
        storedResourcesMode(){
            const mode = this.activeTab === 'resource-list' ? null : 'flat';
            return mode;
        },
        addResourcesMode(){
            const mode = this.activeTab === 'add-resource' ? null : 'flat';
            return mode;
        }
    }
}
</script>
<style>
    
</style>