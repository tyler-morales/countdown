<template>
  <div class="cards">
    <CountdownCard
      v-for="(event, index) in filteredEvents"
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
          year: 2020,
          month: 8,
          day: 22,
          hour: 0,
          minute: 0
        },
        {
          title: 'Winter',
          date: 'December 21, 2020',
          emoji: '⛄️',
          year: 2020,
          month: 11,
          day: 21,
          hour: 0,
          minute: 0
        }
      ],
      updateSearch: ''
    }
  },
  mounted() {
    EventBus.$on('search-countdowns', search => {
      this.updateSearch = search
    })
  },
  computed: {
    filteredEvents: function() {
      return this.events.filter(event => {
        return event.title.match(this.updateSearch)
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
