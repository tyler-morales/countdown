<template>
  <button @click="emitFilter">{{ filter.name }}</button>
</template>

<script>
import EventBus from '@/components/EventBus'

export default {
  props: {
    filter: {
      type: Object,
      required: true
    }
  },
  data() {
    return {
      filterResult: ''
    }
  },
  methods: {
    emitFilter() {
      this.filterResult = this.filter.type
      EventBus.$emit('filter-catagories', this.filterResult)
    }
  }
}
</script>

<style lang="scss" scoped>
button {
  padding: 5px 30px;
  border-radius: 20px;
  background-color: var(--color-primary);
  color: #fff;
  font-size: 24px;
  transition: all 0.3s;

  &:hover {
    transform: translateY(-1px);
  }
}
</style>
