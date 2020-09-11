<template>
  <div class="bg-gray-100 min-h-screen">
    <div class="container mx-auto px-3 py-6">
      <h1 class="mb-3 text-xl font-bold">Use this app to get some Cat Facts</h1>
      <div class="mb-3">
        <label 
          for="number"
          class="text-sm"
        >
          Type number of facts to retrieve (max 10)
        </label>
        <input
          id="number"
          v-model="number"
          type="number"
          min="1"
          max="10"
          class="w-16 ml-2 p-3 border rounded"
        >
      </div>
      <button
        class="mb-3 p-3 font-bold text-white rounded bg-blue-500 hover:bg-blue-600"
        :disabled="loading"
        @click="submit"
      >
        {{ loading ? 'Loading' : 'Get cat fact(s)!' }}
      </button>
      <p v-if="!results.length">
        No results, try hitting the button above
      </p>
      <ul 
        v-else
        class="sm:w-1/2 lg:w-1/3"
      >
        <li
          is="FactTile"
          v-for="fact in results"
          :key="fact._id"
          :fact="fact"
          class="mb-3"
        />
      </ul>
    </div>
  </div>
</template>

<script>
import catFacts from 'get-cat-facts'
import FactTile from '~/components/FactTile'

export default {
  components: {
    FactTile
  },

  data() {
    return {
      loading: false,
      results: [],
      number: 1
    }
  },

  methods: {
    async submit() {
      this.loading = true
      try {
        const results = await catFacts.random(this.number)
        if (Array.isArray(results)) {
          this.results = results
        } else {
          this.results = [results]
        }
      } catch(error) {
        console.log(error)
      }
      this.loading = false
    }
  }
}
</script>

<style>

</style>