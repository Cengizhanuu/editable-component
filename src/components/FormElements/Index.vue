<template>
  <div class="item">
    <SingleInput v-if="type === 1" :validation="validation" :label="label" :url="url" />
    <MultipleInput v-if="type === 2" :validation="validation" :label="label" :url="url" />
    <Datepicker v-if="type === 3" :validation="validation" :label="label" :url="url" />
    <NumberInput v-if="type === 4" :validation="validation" :label="label" :url="url" />
  </div>
</template>
<script>
import SingleInput from './SingleInput/SingleInput.vue'
import MultipleInput from './MultipleInput/MultipleInput.vue'
import Datepicker from './Datepicker/Datepicker.vue'
import NumberInput from './NumberInput/NumberInput.vue'

export default {
  props: ['type', 'validation', 'label', 'url'],
  components: {
    SingleInput,
    MultipleInput,
    Datepicker,
    NumberInput
  }
}
</script>