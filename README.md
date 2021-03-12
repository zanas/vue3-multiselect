# vue3-multiselect
A Vue 3 upgrade of [@shentao's](https://github.com/shentao) [vue-mulitselect](https://github.com/shentao/vue-multiselect) component.
The idea is that when you upgrade to Vue 3, you can swap the two components out, and everything should simply work.

Feel free to check out our story of how we upgraded our product to Vue 3 on our blog at  [suade.org](https://suade.org/dev/a-products-vue-3-migration-a-real-life-story/)

## Features & characteristics:
* NO dependencies
* Single select
* Multiple select
* Tagging
* Dropdowns
* Filtering
* Search with suggestions
* Logic split into mixins
* Basic component and support for custom components
* V-model support
* Vuex support
* Async options support
* Fully configurable (see props list below)


## Install & basic usage

```bash
npm install vue3-multiselect
```

```vue
<template>
  <div>
    <multiselect
      v-model="selected"
      :options="options">
    </multiselect>
  </div>
</template>

<script>
  import Multiselect from 'vue3-multiselect'
  export default {
    components: { Multiselect },
    data () {
      return {
        selected: null,
        options: ['list', 'of', 'options']
      }
    }
  }
</script>

<style src="vue3-multiselect/dist/vue3-multiselect.min.css"></style>
```

## Examples
in jade-lang/pug-lang

### Single select / dropdown
``` jade
multiselect(
  :model-value="value",
  :options="source",
  :searchable="false",
  :close-on-select="false",
  :allow-empty="false",
  @update:model-value="updateSelected",
  label="name",
  placeholder="Select one",
  track-by="name"
)
```

### Single select with search
``` jade
multiselect(
  v-model="value",
  :options="source",
  :close-on-select="true",
  :clear-on-select="false",
  placeholder="Select one",
  label="name",
  track-by="name"
)
```

### Multiple select with search
``` jade
multiselect(
  v-model="multiValue",
  :options="source",
  :multiple="true",
  :close-on-select="true",
  placeholder="Pick some",
  label="name",
  track-by="name"
)
```

### Tagging
with `@tag` event
``` jade
multiselect(
  v-model="taggingSelected",
  :options="taggingOptions",
  :multiple="true",
  :taggable="true",
  @tag="addTag",
  tag-placeholder="Add this as new tag",
  placeholder="Type to search or add tag",
  label="name",
  track-by="code"
)
```

``` javascript

addTag (newTag) {
  const tag = {
    name: newTag,
    code: newTag.substring(0, 2) + Math.floor((Math.random() * 10000000))
  }
  this.taggingOptions.push(tag)
  this.taggingSelected.push(tag)
},
```

### Asynchronous dropdown
``` jade
multiselect(
  v-model="selectedCountries",
  :options="countries",
  :multiple="multiple",
  :searchable="searchable",
  @search-change="asyncFind",
  placeholder="Type to search",
  label="name"
  track-by="code"
)
  span(slot="noResult").
    Oops! No elements found. Consider changing the search query.
```

``` javascript
methods: {
  asyncFind (query) {
    this.countries = findService(query)
  }
}
```

## Contributing

``` bash
# distribution build with minification
npm run bundle

# run unit tests
npm run test

```

