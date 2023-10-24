<template>
  <div class="datepicker border p-2 rounded">   
    <div v-if="!edit" class="flex items-center justify-center">
      <p class="w-full cursor-pointer p-2" @click="openEdit">{{ inputVal }}</p>
      <button type="button" class="underline ml-2 cursor-pointer font-bold"  @click="openEdit">Edit</button> 
    </div>
    <div class="flex items-center justify-center" v-else>  
      <input type="date" v-model="inputVal" class="border w-full border-black outline-0 p-2 rounded" />
      <button @click="saveEdit" type="button" class="underline ml-2 cursor-pointer font-bold">Save</button> 
    </div> 
    <div v-if="error" class="error">  
      <p class="text-red-600">Selecting a date is required.</p> 
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
      if(this.inputVal === '' || this.inputVal === ''){  
        this.error = true
        return false    
      }else{
        this.error = false
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
    }
  }
}
</script>