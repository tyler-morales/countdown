<template>
  <div id="app">
    <Header />
    <div class="content">
      <Filters />
      <SearchCountdowns />
      <CardContainer />
    </div>
  </div>
</template>

<script>
import Filters from '@/components/Filters'
import Header from '@/components/Header'
import CardContainer from '@/components/CardContainer'
import SearchCountdowns from '@/components/SearchCountdowns'

export default {
  name: 'App',
  components: {
    Header,
    Filters,
    CardContainer,
    SearchCountdowns
  }
}
</script>

<style lang="scss">
.content {
  width: 80vw;
  margin: 0 auto;
  margin-top: 100px;
}
</style>
