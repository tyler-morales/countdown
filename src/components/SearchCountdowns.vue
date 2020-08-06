<template>
  <input
    type="text"
    v-model="search"
    placeholder="Search Countdowns"
    @keyup="emitGlobalKeyupSearch()"
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
    emitGlobalKeyupSearch() {
      this.search
      EventBus.$emit('search-countdowns', this.search)
    }
  }
}
</script>

<style lang="scss" scoped>
input {
  // margin-top: 20px;
  font-size: 24px;
  border-radius: 20px;
  padding: 10px 20px;
  box-shadow: var(--shadow-md);
  // width: 100%;
  flex: 1;
}
</style>
