<template>
    <li :key="id">
        <base-card>
            <header>
                <h3>{{ title }}</h3>
                <base-button mode="flat" @click="deleteHandler">Delete</base-button>
            </header>
            <p>{{ description }}</p>
            <nav>
                <a :href="link"> View Resource</a>
            </nav>
        </base-card>
    </li>
</template>
<script>
import BaseButton from '../UI/BaseButton.vue'
export default{
  components: { BaseButton },
    props:{
        id:{
            type:String,
            required:true
        },
        title:{
            type:String,
            required:true
        },
        description:{
            type:String,
            required:true
        },
        link:{
            type:String,
            required:true
        }
    },
    inject:['deleteResource'],
    methods:{
      deleteHandler(){
        this.deleteResource(this.id)
      }
    }

}
</script>


<style >
li {
  margin: auto;
  max-width: 40rem;
}

header {
  display: flex;
  justify-content: space-between;
  align-items: center;
}

h3 {
  font-size: 1.25rem;
  margin: 0.5rem 0;
}

p {
  margin: 0.5rem 0;
}

a {
  text-decoration: none;
  color: #ce5c00;
}

a:hover,
a:active {
  color: #c89300;
}
</style>