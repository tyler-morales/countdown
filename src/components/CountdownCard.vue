<template>
  <div class="card">
    <h3 class="card--title">{{ event.title }}</h3>
    <h3 class="card--date">{{ event.date }}</h3>
    <span class="card--emoji">{{ event.emoji }}</span>
    <Timer
      :year="event.year"
      :month="event.month"
      :day="event.day"
      :hour="event.hour"
      :minute="event.minute"
      :second="event.second"
      :milliseconds="event.milliseconds"
    />
  </div>
</template>

<script>
import Timer from '@/components/Timer'

export default {
  props: {
    event: {
      type: Object,
      required: true
    }
  },
  components: {
    Timer
  }
}
</script>

<style lang="scss" scoped>
.card {
  font-family: var(--body-text);
  text-align: center;
  font-weight: 400;
  box-shadow: var(--shadow-lg);
  width: min-content;
  padding: 20px 30px;
  border-radius: 20px;
  background-color: #fff;

  &--title {
    color: var(--color-primary);
    margin-bottom: 10px;
  }

  &--date {
    color: var(--color-gray);
    margin-bottom: 15px;
    font-weight: 400;
  }
  &--emoji {
    font-size: 140px;
    padding: 0 20px;
    border-radius: 20px;
    background-color: var(--color-lightgray);
  }
}
</style>
