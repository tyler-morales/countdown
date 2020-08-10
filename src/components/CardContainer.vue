<template>
  <div class="cards">
    <CountdownCard
      v-for="(event, index) in filteredItems"
      :key="index"
      :event="event"
    />
    <div
      class="createEventBox"
      v-if="customCount == 0 && this.filter == 'custom'"
    >
      <h1>You haven't created any events. Create one!</h1>
      <button>Create Event</button>
    </div>
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
          arrDate: new Date('2020-08-22'),
          emoji: '🍂',
          type: 'season',
          year: 2020,
          month: 8,
          day: 21,
          hour: 0,
          minute: 0
        },
        {
          title: 'Winter',
          date: 'December 21, 2020',
          arrDate: new Date('2020-12-21'),
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
          date: 'October 31, 2020',
          arrDate: new Date('2020-10-31'),
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
      sort: 'alpha',
      customCount: 0
    }
  },
  mounted() {
    this.events.forEach(event => {
      if (event.type == 'custom') {
        this.customCount++
      }
    })
    EventBus.$on('search-countdowns', search => {
      this.updateSearch = search
    }),
      EventBus.$on('filter-catagories', filter => {
        this.filter = filter
      }),
      EventBus.$on('sort-catagories', sort => {
        this.sort = sort
      })
  },
  computed: {
    filteredItems: function() {
      return (
        this.events
          // filters at work
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
            if (this.sort == 'timeLeast') {
              return a.arrDate - b.arrDate
            }
            if (this.sort == 'timeMost') {
              return b.arrDate - a.arrDate
            }
            // default sort: alphabetically
            return a.title.localeCompare(b.title)
          })
      )
    }
  }
}
</script>

<style lang="scss" scoped>
.createEventBox {
  margin: 0 auto;
  display: flex;
  justify-content: center;
  flex-direction: column;
  text-align: center;
}
.cards {
  display: flex;
  flex-wrap: wrap;
  gap: 84px;
  margin-top: 50px;
}
</style>
