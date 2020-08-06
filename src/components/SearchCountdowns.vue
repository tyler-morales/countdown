<template>
  <input
    type="text"
    v-model="search"
    placeholder="Search Countdowns"
    @change="emitGlobalClickEvent()"
  />
</template>

<script>
import EventBus from '@/components/EventBus'
export default {
  data() {
    return {
      search: ''
    }
  },
  methods: {
    emitGlobalClickEvent() {
      this.search
      EventBus.$emit('search-countdowns', this.search)
    }
  }
}
</script>

<style lang="scss" scoped></style>
