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
          emoji: '❄️',
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
        },
        {
          title: 'Spring',
          date: 'March 20, 2020',
          arrDate: new Date('2021-3-20'),
          emoji: '🌸',
          type: 'season',
          year: 2021,
          month: 2,
          day: 20,
          hour: 0,
          minute: 0
        },
        {
          title: 'Summer',
          date: 'June 20, 2021',
          arrDate: new Date('2021-6-20'),
          emoji: '🌞',
          type: 'season',
          year: 2021,
          month: 5,
          day: 20,
          hour: 0,
          minute: 0
        },
        {
          title: "New Year's Day",
          date: 'January 1, 2021',
          arrDate: new Date('2021-1-1'),
          emoji: '🎊',
          type: 'holiday',
          year: 2021,
          month: 0,
          day: 1,
          hour: 0,
          minute: 0
        },
        {
          title: 'Martin Luther King Jr. Day',
          date: 'January 20, 2021',
          arrDate: new Date('2021-1-20'),
          emoji: '👨🏾‍🏫',
          type: 'holiday',
          year: 2021,
          month: 0,
          day: 20,
          hour: 0,
          minute: 0
        },
        {
          title: "Presidents' Day",
          date: 'Febuary 20, 2021',
          arrDate: new Date('2021-2-17'),
          emoji: '🤵',
          type: 'holiday',
          year: 2021,
          month: 1,
          day: 17,
          hour: 0,
          minute: 0
        },
        {
          title: 'Independence Day',
          date: 'July 4, 2021',
          arrDate: new Date('2021-7-4'),
          emoji: '🎆',
          type: 'holiday',
          year: 2021,
          month: 6,
          day: 4,
          hour: 0,
          minute: 0
        },
        {
          title: 'Labor Day',
          date: 'September 7, 2020',
          arrDate: new Date('2020-9-7'),
          emoji: '💼',
          type: 'holiday',
          year: 2020,
          month: 8,
          day: 7,
          hour: 0,
          minute: 0
        },
        {
          title: 'Veterans Day',
          date: 'November 11, 2021',
          arrDate: new Date('2021-11-11'),
          emoji: '🇺🇸',
          type: 'holiday',
          year: 2021,
          month: 10,
          day: 11,
          hour: 0,
          minute: 0
        },
        {
          title: 'Thanksgiving Day',
          date: 'November 26, 2020',
          arrDate: new Date('2020-11-26'),
          emoji: '🦃',
          type: 'holiday',
          year: 2020,
          month: 10,
          day: 11,
          hour: 0,
          minute: 0
        },
        {
          title: 'Christmas Day',
          date: 'December 25, 2020',
          arrDate: new Date('2020-12-25'),
          emoji: '🎅🏼',
          type: 'holiday',
          year: 2020,
          month: 11,
          day: 25,
          hour: 0,
          minute: 0
        }
      ],
      updateSearch: '',
      filter: 'all',
      sort: 'timeLeast',
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
            if (this.sort == 'alpha') {
              return a.title.localeCompare(b.title)
            }
            if (this.sort == 'timeMost') {
              return b.arrDate - a.arrDate
            }
            // default sort: alphabetically
            return a.arrDate - b.arrDate
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
  justify-content: center;

  @include breakpoint(sm) {
    gap: 40px;
  }
}
</style>
