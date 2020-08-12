<template>
  <div id="app">
    <Header />
    <div class="content">
      <Filters />
      <CardContainer />
    </div>
    <Footer />
  </div>
</template>

<script>
import Filters from '@/components/Filters'
import Header from '@/components/Header'
import CardContainer from '@/components/CardContainer'
import Footer from '@/components/Footer'

export default {
  name: 'App',
  components: {
    Header,
    Filters,
    CardContainer,
    Footer
  }
}
</script>

<style lang="scss">
.content {
  width: 80vw;
  margin: 0 auto;
  margin-top: 100px;

  @include breakpoint(sm) {
    margin: 20px auto;
    width: 90vw;
  }
}
</style>
