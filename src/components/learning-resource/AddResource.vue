<template>
    <base-dialog v-if="isInvalidInputs" title="Invalalid Inputs" @close="confirmError">
        <template #default>
            <p>Unfortunately, at least one input value is invalid.</p>
            <p>Please check all inputs and make sure you enter at least a few characters into each input field.</p>
        </template>
        <template #actions>
            <base-button @click="confirmError">Okay !</base-button>
        </template>
    </base-dialog>
    <base-card>
        <form @submit.prevent="saveData">
            <div class="form-control">
                <label for="title">Title</label>
                <input type="text" name="title" id="title" ref="title">
            </div>
            <div class="form-control">
                <label for="description">Description</label>
                <textarea name="description" id="description" rows="3" ref="description"></textarea>
            </div>
            <div class="form-control">
                <label for="link">Link</label>
                <input type="url" name="link" id="link" ref="link">
            </div>
            <base-button type="submit">Add Resource</base-button>
        </form>
    </base-card>
</template>
<script>
import BaseDialog from '../UI/BaseDialog.vue';
export default {
    components : {
        BaseDialog,
    },
    data(){
        return {
            isInvalidInputs  : false,
        }
    },
    inject : ['addResource' , 'changeTab'],
    methods: {
        saveData(){
            const id = new Date().toISOString();
            const title = this.$refs.title.value;
            const description = this.$refs.description.value;
            const link = this.$refs.link.value;
            // add control

            if(title.trim() === ''
                ||
                description.trim() === ''
                || 
                link.trim() === ''
            ){
                this.isInvalidInputs = true;
                return;
            }

            const data = { id : id , title : title , description : description , link : link };
            this.addResource(data);
            this.changeTab();
            
        },
        confirmError(){
            this.isInvalidInputs = false;
        }
        
    },
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