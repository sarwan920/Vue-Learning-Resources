<template>
 <base-dialog v-if="inputIsInvalid" title="Invalid Input" @close="confirmError">
 <template #default>
   <p>Your Input Is Invalid!</p>
   <p>Please Check all The Inputs.</p>
 </template>

 <template #actions>
   <base-button @click="confirmError">Okay!</base-button>
 </template>
 </base-dialog>
  <base-card>
    <form @submit.prevent="onSubmit" >
      <div class="form-control">
        <label for="title">Title</label>
        <input id="title"   name="title" type="text" ref="titleInput" />
      </div>

      <div class="form-control">
        <label for="description">Title</label>
        <textarea name="description"  id="description" rows="3" ref="descInput"></textarea>
      </div>

      <div class="form-control">
        <label for="link">Link</label>
        <input id="link" name="link" ref="linkInput" type="url" />
      </div>

      <div>
          <base-button type="submit">
          Add Resource
          </base-button>
      </div>
    </form>
  </base-card>
 
</template>

<script>
export default {
  inject:['addResource'],
  data(){
    return{
     inputIsInvalid:false
    }
  },
  methods:{
    onSubmit(){
     const enteredTitle=this.$refs.titleInput.value;
     const enteredDesc=this.$refs.descInput.value;
     const enteredLink=this.$refs.linkInput.value;

     if(enteredTitle.trim()==='' || enteredDesc.trim()==='' || enteredLink.trim()===''){
       this.inputIsInvalid=true;
       return;
     }
     this.addResource(enteredTitle,enteredDesc,enteredLink);
    },
    confirmError(){
      this.inputIsInvalid=false;
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