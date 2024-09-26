<template>
        <ul>
            <learn-resource 
                v-for="resource in resources"
                :key="resource.id"
                :id="resource.id"
                :title="resource.title"
                :description="resource.description"
                :link="resource.link"
            >
            </learn-resource>
        </ul>
</template>
<script>
import LearnResource from './LearnResource.vue';
export default {
    inject:['resources'],
    components:{
        LearnResource
    }
}
</script>

<style scoped>
ul {
  list-style: none;
  margin: 0;
  padding: 0;
  margin: auto;
  max-width: 40rem;
}
</style>