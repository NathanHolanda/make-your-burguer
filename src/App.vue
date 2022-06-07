<template>
  <Navbar />
  <router-view/>
  <Footer />
</template>

<style>
  *{
    padding: 0;
    margin: 0;
    box-sizing: border-box;
    font-family: Helvetica, Arial, sans-serif;
  }

  .main-container{
    margin: 50px;
    min-height: 250px;
  }
</style>

<script>
  import Navbar from "./components/Navbar.vue"
  import Footer from "./components/Footer.vue"

  export default {
    components: {
      Navbar,
      Footer
    }
  }
</script>
