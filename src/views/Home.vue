<template>
  <main class="p-8">
    <FormElements class="mb-2" :type="1" :validation="{min: 2, max: 64}" :label="'Test123'" :url="'https://jsonplaceholder.typicode.com/todos/1'" />
    <FormElements class="mb-2" :type="2" :validation="{min: 2, max: 64}" :label="'Test123'" :url="'https://jsonplaceholder.typicode.com/todos/1'" /> 
    <FormElements class="mb-2" :type="3" :validation="{min: 2, max: 64}" :label="'2023-01-01'" :url="'https://jsonplaceholder.typicode.com/todos/1'" />
    <FormElements class="mb-2" :type="4" :validation="{min: 2, max: 64}" :label="222" :url="'https://jsonplaceholder.typicode.com/todos/1'" /> 
    <FormElements class="mb-2" :type="4" :validation="{min: 2, max: 64}" :label="22" :url="'https://jsonplaceholder.typicode.com/todos/1'" />
  </main>     
</template>     
<script>
import FormElements from '../components/FormElements/Index.vue'

export default {
  components: {
    FormElements
  }
}
</script>
