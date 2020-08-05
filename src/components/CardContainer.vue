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
  data() {
    return {
      events: [
        {
          title: 'Autum',
          date: 'September 22, 2020',
          emoji: '🍂',
          daysLeft: 35,
          hoursLeft: 12
        }
      ]
    }
  },
  components: {
    CountdownCard
  }
}
</script>

<style lang="scss" scoped>
.cards {
  // display: grid;
  // grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
  display: flex;
  flex-wrap: wrap;
  gap: 84px;
  margin-top: 50px;
}
</style>
