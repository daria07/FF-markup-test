<template>
    <Header />
    <router-view/>
    <Footer />
</template>

<style lang="scss">
  @import url(assets/css/style.css);
</style>

<script>
  import Header from './components/Header';
  import Footer from './components/Footer'

  export default ({
    components: {Header, Footer}
  })
</script>
