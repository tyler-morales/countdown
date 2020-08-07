<template>
  <div>
    <span>filters</span>
    <div class="filter-bar">
      <FilterBtn />
      <Dropdown :menuLabel="menuLabel" :choices="myChoices"></Dropdown>
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
  display: flex;
  justify-content: center;
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
