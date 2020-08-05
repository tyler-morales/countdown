<template>
  <div class="card">
    <h3 class="card--title">{{ event.title }}</h3>
    <h3 class="card--date">{{ event.date }}</h3>
    <span class="card--emoji">{{ event.emoji }}</span>
    <div class="card__countdown">
      <div class="card__countdown__num">
        <span class="card__countdown__num--time">{{ event.daysLeft }}</span>
        <span class="card__countdown__num--unit">Days</span>
      </div>
      <span class="card__countdown__num--colon">:</span>
      <div class="card__countdown__num">
        <span class="card__countdown__num--time">{{ event.hoursLeft }}</span>
        <span class="card__countdown__num--unit">Hours</span>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    event: {
      type: Object,
      required: true
    }
  }
}
</script>

<style lang="scss" scoped>
.card {
  font-family: var(--body-text);
  text-align: center;
  font-weight: 400;
  box-shadow: var(--shadow-light);
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

  &__countdown {
    display: flex;
    justify-content: space-evenly;
    margin-top: 20px;

    &__num {
      display: flex;
      flex-direction: column;

      &--time {
        color: var(--color-primary);
        font-size: 40px;
      }
      &--unit {
        color: var(--color-gray);
        font-size: 12;
      }
      &--colon {
        color: var(--color-primary);
        font-size: 40px;
        line-height: 1.4em;
      }
    }
  }
}
</style>
