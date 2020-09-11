<template>
  <div class="shadow-sm rounded p-3 bg-white">
    <p class="text-sm italic text-gray-600">{{ `Last updated ${date}` }}</p>
    <p class="font-bold">{{ fact.text }}</p>
  </div>
</template>

<script>
import moment from 'moment'

export default {
  props: {
    fact: {
      type: Object,
      required: true
    }
  },

  computed: {
    date() {
      return moment(String(this.fact.updatedAt)).format('DD/MM/YYYY hh:mm')
    }
  }
}
</script>

<style>

</style>