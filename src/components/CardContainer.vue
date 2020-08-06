<template>
  <div class="cards">
    <CountdownCard
      v-for="(event, index) in events"
      :key="index"
      :event="event"
    />
  </div>
</template>

<script>
import CountdownCard from '@/components/CountdownCard'

export default {
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
          minute: 0,
          second: 0,
          milliseconds: 0
        },
        {
          title: 'Winter',
          date: 'December 21, 2020',
          emoji: '⛄️',
          year: 2020,
          month: 11,
          day: 21,
          hour: 0,
          minute: 0,
          second: 0,
          milliseconds: 0
        }
      ]
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
