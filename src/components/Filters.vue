<template>
  <div>
    <span>filters</span>
    <div class="filter-bar">
      <FilterBtn
        v-for="(filter, index) in filters"
        :key="index"
        :filter="filter"
      />
    </div>
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
.filter-bar {
  display: flex;
  flex-wrap: wrap;
  gap: 45px;
  margin-top: 15px;
}
span {
  text-transform: uppercase;
  font-size: 12px;
  color: var(--color-gray);
  font-family: var(--header-text);
  font-weight: 500;
  letter-spacing: 2px;
  display: block;
}
</style>
