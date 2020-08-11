<template>
  <div>
    <div class="filter-bar">
      <div class="filter-bar__filters">
        <span class="filter-category">filters</span>
        <FilterBtn />
      </div>
      <div class="filter-bar__sort">
        <span class="filter-category">sort</span>
        <Dropdown :menuLabel="menuLabel" :choices="myChoices" />
      </div>
      <SearchCountdowns />
    </div>
  </div>
</template>

<script>
import FilterBtn from '@/components/FilterBtn'
import SearchCountdowns from '@/components/SearchCountdowns'
import Dropdown from '@/components/Dropdown'

export default {
  components: {
    FilterBtn,
    SearchCountdowns,
    Dropdown
  },
  data: function() {
    return {
      myChoices: [
        { label: 'Alphabetically', name: 'alpha' },
        { label: 'Time Left (least)', name: 'timeLeast' },
        { label: 'Time Left (most)', name: 'timeMost' }
      ],
      menuLabel: 'SortDropdown'
    }
  }
}
</script>

<style lang="scss" scoped>
.filter-bar {
  grid-template-columns: repeat(2, max-content);
  display: grid;
  flex-wrap: wrap;
  gap: 45px;
  margin-top: 15px;

  @include breakpoint(lg) {
    grid-template-columns: max-content;
  }

  @include breakpoint(md) {
    grid-template-columns: 1fr;
  }
}
.filter-category {
  text-transform: uppercase;
  font-size: 12px;
  color: var(--color-gray);
  font-family: var(--header-text);
  font-weight: 500;
  letter-spacing: 2px;
  display: block;
  margin-bottom: 10px;
}
</style>
