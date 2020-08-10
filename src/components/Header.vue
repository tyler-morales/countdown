<template>
  <header>
    <div class="header__text">
      <img src="@/assets/logo.png" alt="logo" />
      <h1>Tick'it</h1>
      <span
        >The all in one countdown timer for all of your most important
        moments!</span
      >
    </div>
  </header>
</template>

<script>
export default {}
</script>

<style lang="scss" scoped>
header {
  padding: 15px 0;

  background-color: var(--color-primary);
  color: white;

  img {
    width: 50px;
    height: auto;
  }

  .header__text {
    max-width: 80vw;
    display: flex;
    gap: 30px;
    align-items: center;
    margin: 0 auto;

    h1 {
      font-family: var(--header-text);
      font-size: 35px;
      font-weight: 700;
    }
    span {
      font-family: var(--body-text);
      font-size: 18px;

      @include breakpoint(sm) {
        display: none;
      }
    }
  }
}
</style>
