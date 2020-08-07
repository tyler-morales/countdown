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
          title: 'Christmas',
          date: 'December 25, 2020',
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
          year: 2020,
          month: 8,
          day: 14,
          hour: 0,
          minute: 0
        }
      ],
      updateSearch: '',
      filter: 'all'
    }
  },
  mounted() {
    return (
      EventBus.$on('search-countdowns', search => {
        this.updateSearch = search
      }),
      EventBus.$on('filter-catagories', filter => {
        this.filter = filter
      })
    )
  },
  computed: {
    filteredItems: function() {
      // initial population
      if (this.filter == 'all') {
        return this.events
      }
      // filters at work
      if (this.filter != 'All') {
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
              return event.type == this.filter
            })
        )
      }
      return this.events
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
