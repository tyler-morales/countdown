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
  background-color: var(--color-primary-light);
  color: var(--color-primary);
  font-size: 24px;
  transition: all 0.2s;
  margin-right: 20px;
  border: 3px solid transparent;

  &:hover {
    transform: translateY(-3px);
    box-shadow: var(--shadow-base);
    color: rgba(var(--color-text-black), 1);
    background-color: #fff;
  }

  @include breakpoint(sm) {
    width: 100%;
    margin-right: 0;
    margin-bottom: 15px;
  }
}
</style>
