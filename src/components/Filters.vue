<template>
  <div>
    <FilterBtn v-for="(title, index) in filters" :key="index" :title="title" />
  </div>
</template>

<script>
import FilterBtn from '@/components/FilterBtn'

export default {
  components: {
    FilterBtn
  },
  data() {
    return {
      filters: [
        { name: 'All' },
        { name: 'Holidays' },
        { name: 'Seasons' },
        { name: 'Events' }
      ]
    }
  }
}
</script>

<style lang="scss" scoped>
div {
  display: flex;
  flex-wrap: wrap;
  gap: 45px;
}
</style>
