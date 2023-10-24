<template>
  <div class="numberInput border p-2 rounded">
    <div v-if="!edit" class="flex items-center justify-center">
      <p class="w-full cursor-pointer p-2" @click="openEdit">{{ inputVal }}</p>
      <button type="button" class="underline ml-2 cursor-pointer font-bold"  @click="openEdit">Edit</button> 
    </div>
    <div class="flex items-center justify-center" v-else>
      <input @input="checkValidate" v-model="inputVal" class="border w-full border-black outline-0 p-2 rounded" type="number">
      <button @click="saveEdit" type="button" class="underline ml-2 cursor-pointer font-bold">Save</button>   
    </div> 
    <div v-if="error" class="error"> 
      <p class="text-red-600">{{`The number entered must be between ${validation.min} and ${validation.max}.`}}</p> 
    </div>
  </div>  
</template>
<script>
export default {
  props: ['validation', 'label', 'url'],
  data(){
    return {
      edit: false,
      inputVal: this.label ? this.label:'',
      error: false
    }
  },
  methods: {
    openEdit(){ 
      this.edit = true
      this.checkValidate()
    },
    saveEdit(){     
      if(this.error){
        return false
      }
      fetch(this.url, {
        method:"POST",
        body: JSON.stringify({ 
          input: this.inputVal
        })
      })  
      .then(response => response.json())
      .then(json => console.log(json))
      this.edit = false
    },
    checkValidate(){   
      if (this.inputVal < this.validation.min || this.inputVal > this.validation.max) {
        this.error = true;
      } else {
        this.error = false;
      }
    },
  },
  mounted(){ 
    if (this.inputVal < this.validation.min || this.inputVal > this.validation.max) {
      this.inputVal = 0
      this.error = true;
    } else {
      this.error = false;
    }
  }
}
</script>