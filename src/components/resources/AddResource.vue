<template>
    <base-dialog v-if="isInputInvalid" title="Invalid Input" @close="confirmError">
        <template #default>
            <p>Unfortunately, at least one input is invalid!</p>
            <p>Please check all inputs and make sure you have entered all data.</p>
        </template>
        <template #actions>
            <base-button @click="confirmError">Okay</base-button>
        </template>
    </base-dialog>
    
    <base-card>
    <form action="submit" @submit.prevent="submitData">
        <div class="form-control">
            <label for="title">Title:</label>
            <input type="text" name="title" id="title" ref="titleInput">
        </div>
        <div class="form-control">
            <label for="description">Description:</label>
            <textarea type="text" name="description" id="description" ref="descInput"></textarea>
        </div>
        <div class="form-control">
            <label for="link">Link:</label>
            <input type="URL" name="link" id="link" ref="linkInput">
        </div>
        <div>
            <base-button type="submit">Add Resource</base-button>
        </div>
    </form>
    </base-card>
</template>


<script>
import BaseButton from '../UI/BaseButton.vue'
    export default {
  components: { BaseButton },
        data() {
            return {
                isInputInvalid: false,
            }  
        },
        methods: {
            submitData() {
                const enteredTitle = this.$refs.titleInput.value
                const enteredDesc = this.$refs.descInput.value
                const enteredUrl = this.$refs.linkInput.value
                if (enteredTitle.trim() === '' || enteredDesc.trim() === '' || enteredUrl.trim() === '') {
                    this.isInputInvalid = true
                    return
                }
                this.addResource(enteredTitle, enteredDesc, enteredUrl)
            },
            confirmError() {
                this.isInputInvalid = false;
            }
        },
        inject: ['addResource']
        
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