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
          title: 'Autum',
          date: 'September 22, 2020',
          emoji: '🍂',
          type: 'season',
          year: 2020,
          month: 8,
          day: 22,
          hour: 0,
          minute: 0
        },
        {
          title: 'Winter',
          date: 'December 21, 2020',
          emoji: '🎄',
          type: 'season',
          year: 2020,
          month: 11,
          day: 21,
          hour: 0,
          minute: 0
        },
        {
          title: 'Halloween',
          date: 'October 13, 2020',
          emoji: '🎃',
          type: 'holiday',
          year: 2020,
          month: 9,
          day: 31,
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
      // filters at work
      return (
        this.events
          // search filter
          .filter(event => {
            return event.title
              .toLowerCase()
              .includes(this.updateSearch.toLowerCase())
          })
          // category filters
          .filter(event => {
            if (this.filter == '' || this.filter == 'all') {
              return this.events
            } else {
              return event.type == this.filter
            }
          })
          .sort((a, b) => {
            if (this.sort == 'alpha') {
              return a.title.localeCompare(b.title)
            }
            if (this.sort == 'timeLeast') {
              return a.month - b.month // https://stackoverflow.com/q/1063007/
            }
            if (this.sort == 'timeMost') {
              return b.month - a.month // https://stackoverflow.com/q/1063007/
            }
            // what's the default sort?
          })
      )
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
