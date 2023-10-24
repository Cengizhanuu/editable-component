<template>
  <div class="multipleInput border p-2 rounded">   
    <div v-if="!edit" class="flex items-center justify-center">  
      <p v-html="multiLineTextWithLineBreaks" class="w-full cursor-pointer p-2" @click="openEdit"></p>
      <button type="button" class="underline ml-2 cursor-pointer font-bold"  @click="openEdit">Edit</button> 
    </div>
    <div class="flex items-center justify-center" v-else>
      <textarea @input="checkValidate" rows="5" cols="30" :maxlength="validation.max" v-model="inputVal" class="border w-full border-black outline-0 p-2 rounded" />
      <div class="ml-1" v-text="(validation.max - inputVal.length)"></div>
      <button @click="saveEdit" type="button" class="underline ml-2 cursor-pointer font-bold">Save</button> 
    </div> 
    <div v-if="error" class="error">
      <p class="text-red-600">{{`The number of characters entered cannot be less than ${validation.min}.`}}</p>
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
      if(this.inputVal.length < 2){
        this.error = true
      } else {
        this.error = false
      }
    }
  },
  computed: {
    multiLineTextWithLineBreaks() {
      return this.inputVal.replace(/\n/g, "<br>");
    },
  },
}
</script>