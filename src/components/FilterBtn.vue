<template>
  <div>
    <button
      v-for="(filter, index) in filters"
      :key="index"
      :class="{ active: index === activeItem }"
      @click="selectItem(index), emitFilter(filter.type)"
    >
      {{ filter.name }}
    </button>
  </div>
</template>

<script>
import EventBus from '@/components/EventBus'
export default {
  data() {
    return {
      activeItem: 0,
      filterResult: '',
      filters: [
        { name: 'All', type: 'all' },
        { name: 'Holidays', type: 'holiday' },
        { name: 'Seasons', type: 'season' },
        { name: 'Events', type: 'custom' }
      ]
    }
  },
  methods: {
    emitFilter(type) {
      this.filterResult = type
      EventBus.$emit('filter-catagories', this.filterResult)
    },
    selectItem(index) {
      this.activeItem = index
    }
  }
}
</script>

<style lang="scss" scoped>
button {
  font-family: var(--header-text);
  padding: 8px 30px;
  border-radius: 20px;
  background-color: var(--color-primary);
  color: #fff;
  font-size: 24px;
  transition: all 0.3s;
  margin-right: 20px;
  border: 3px solid #fafafa;

  // &:hover {
  //   transform: translateY(-1px);
  // }
}
</style>
