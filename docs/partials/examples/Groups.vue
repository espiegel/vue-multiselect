<template lang="pug">
div
  label.typo__label Groups
  multiselect(
    v-model="value",
    :options="filteredOptions",
    :multiple="true",
    group-values="libs",
    group-label="language",
    placeholder="Type to search",
    track-by="name",
    :internal-search="false",
    @search-change="searchChanged",
    label="name",
  )
    span(slot="noResult").
      Oops! No elements found. Consider changing the search query.
  pre.language-json
    code.
      {{ value  }}
</template>

<script>
import Multiselect from 'vue-multiselect'

export default {
  components: {
    Multiselect
  },
  data () {
    return {
      options: [
        {
          language: 'Javascript',
          libs: [
            { name: 'Vue.js', category: 'Front-end' },
            { name: 'Adonis', category: 'Backend' }
          ]
        },
        {
          language: 'Ruby',
          libs: [
            { name: 'Rails', category: 'Backend' },
            { name: 'Sinatra', category: 'Backend' }
          ]
        },
        {
          language: 'Other',
          libs: [
            { name: 'Laravel', category: 'Backend' },
            { name: 'Phoenix', category: 'Backend' }
          ]
        }
      ],
      filteredOptions: [],
      value: []
    }
  },
  mounted () {
    this.filteredOptions = this.options
  },
  methods: {
    searchChanged (searchQuery, id) {
      var newOptions = this.options.slice()
      newOptions = newOptions.filter(option => option.language.toLowerCase().includes(searchQuery.toLowerCase()))
      this.filteredOptions = newOptions
    }
  }
}
</script>

<style lang="css">
</style>
