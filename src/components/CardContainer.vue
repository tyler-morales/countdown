<template>
  <div class="cards">
    <CountdownCard
      v-for="(event, index) in filteredItems"
      :key="index"
      :event="event"
    />
  </div>
</template>

<script>
import CountdownCard from '@/components/CountdownCard'
import EventBus from '@/components/EventBus'

export default {
  props: {
    milliseconds: {
      default: 0
    },
    seconds: {
      default: 0
    }
  },
  components: {
    CountdownCard
  },
  data() {
    return {
      events: [
        {
          title: 'Yam Kipur',
          date: 'September 22, 2020',
          emoji: '🍂',
          type: 'season',
          year: 2030,
          month: 8,
          day: 22,
          hour: 0,
          minute: 0
        },
        {
          title: 'Christmas',
          date: 'December 25, 2021',
          emoji: '🎅🏼',
          type: 'holiday',
          year: 2020,
          month: 11,
          day: 21,
          hour: 0,
          minute: 0
        },
        {
          title: 'Spring',
          date: 'March 21, 2020',
          emoji: '💐',
          type: 'season',
          year: 2021,
          month: 2,
          day: 21,
          hour: 0,
          minute: 0
        },
        {
          title: "Tyler's Birthday",
          date: 'September 14, 2020',
          emoji: '🎂',
          type: 'custom',
          year: 2022,
          month: 8,
          day: 14,
          hour: 0,
          minute: 0
        },
        {
          title: "Mom's Birthday",
          date: 'December 29, 2020',
          emoji: '🥳',
          type: 'custom',
          year: 2000,
          month: 11,
          day: 29,
          hour: 0,
          minute: 0
        }
      ],
      updateSearch: '',
      filter: 'all',
      sort: 'alpha'
    }
  },
  mounted() {
    return (
      EventBus.$on('search-countdowns', search => {
        this.updateSearch = search
      }),
      EventBus.$on('filter-catagories', filter => {
        this.filter = filter
      }),
      EventBus.$on('sort-catagories', sort => {
        this.sort = sort
      })
    )
  },
  computed: {
    filteredItems: function() {
      let updateSearch = this.updateSearch.toLowerCase() // cached
      return this.events
        .filter(
          (
            event // uses the implicit return of arrow functions
          ) =>
            event.title.toLowerCase().includes(updateSearch) &&
            (this.filter == '' ||
              this.filter == 'all' ||
              event.type == this.filter) // short-circuiting (https://stackoverflow.com/q/12554578/)
        )
        .sort((a, b) => {
          if (this.sort == 'alpha') {
            return a.title.localeCompare(b.title)
          }
          if (this.sort == 'timeLeast') {
            return b.year - a.year // https://stackoverflow.com/q/1063007/
          }
          // what's the default sort?
        })
    }
  }
}
</script>

<style lang="scss" scoped>
.cards {
  display: flex;
  flex-wrap: wrap;
  gap: 84px;
  margin-top: 50px;
}
</style>
