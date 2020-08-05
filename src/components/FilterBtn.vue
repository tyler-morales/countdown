<template>
  <button>{{ title.name }}</button>
</template>

<script>
export default {
  props: {
    title: {
      type: Object,
      required: true
    }
  }
}
</script>

<style lang="scss" scoped>
button {
  padding: 5px 30px;
  border-radius: 20px;
  background-color: var(--color-primary);
  color: #fff;
  font-size: 24px;
  transition: all 0.3s;

  &:hover {
    transform: translateY(-1px);
  }
}
</style>
