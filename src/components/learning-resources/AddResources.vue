<template>
    <base-card>
        <form @submit.prevent="handleSubmit">
            <div class='form-control'>
                <label for="title">Title</label>
                <input id="title" type="text" v-model="newResource.title" />
            </div>
            <div class="form-control">
                <label for="des">Description</label>
                <textarea id="des" v-model="newResource.description" rows="3"></textarea>
            </div>
            <div class="form-control">
                <label for="link">Link</label>
                <input type="url" id="link" v-model="newResource.link"/>
            </div>
            <base-button type="submit">Add Resource</base-button>
        </form>
    </base-card>
    <error-model v-if="invalidInput">
        <teleport to="body">
            <h2>Invalid Input</h2>
            <p v-if="!newResource.title">Please enter the title</p>
            <p v-else-if="!newResource.description">Please enter the description</p>
            <p v-else-if="!newResource.link">Please enter the link</p>
            <button @click="okHandler">okay</button>
        </teleport>
    </error-model>
</template>

<script>
import ErrorModel from './ErrorModel.vue';

export default {
    inject: ['formSubmit'],
    components: {
        ErrorModel
    },
    data() {
        return {
            newResource: {
                id: Math.random().toString(),
                title: '',
                description: '',
                link: ''
            },
            invalidInput: false
        };
    },
    methods: {
        checkInput() {


            if (!this.newResource.title || !this.newResource.description || !this.newResource.link) {
                this.invalidInput = true;
                return false; 
            }
        },
        handleSubmit() {
            if (this.checkInput()) {
                this.formSubmit(this.newResource);
                this.resetForm();
            }
        },
        resetForm() {
            this.newResource = {
                id: Math.random().toString(),
                title: '',
                description: '',
                link: ''
            };
        },
        okHandler(){
            this.invalidInput = false
        }
    }
}
</script>

<style scoped>
label {
    font-weight: bold;
    display: block;
    margin-bottom: 0.5rem;
}

input,
textarea {
    display: block;
    width: 100%;
    font: inherit;
    padding: 0.15rem;
    border: 1px solid #ccc;
}

input:focus,
textarea:focus {
    outline: none;
    border-color: #3a0061;
    background-color: #f7ebff;
}

.form-control {
    margin: 1rem 0;
}
</style>
