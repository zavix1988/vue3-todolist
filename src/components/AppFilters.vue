<template>
  <aside class="app-filters">
    <section class="toggle-group">
      <button
          v-for="filter in filters"
          :key="filter"
          :class="{'button--primary' : activeFilter === filter }"
          @click="setFilter(filter)"
          class="button"
      >{{ filter }}</button>
    </section>
  </aside>
</template>

<script lang="ts">
import {defineComponent, PropType} from 'vue'
import {Filter} from "@/types/Filter";

interface State {
  filters: Filter[]
}

export default defineComponent({
  name: "AppFilters",
  data(): State {
    return {
      filters: ['Active', 'Done', 'All']
    }
  },
  methods: {
    setFilter(filter: Filter) {
      this.$emit('setFilter', filter)
    }
  },
  props: {
    activeFilter: {
      type: String as PropType<Filter>,
      required: true
    }
  },
  emits: {
    setFilter: (filter: Filter) => filter
  }
})
</script>

<style scoped>

</style>