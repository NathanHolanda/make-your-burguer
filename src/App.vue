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
    background-color: rgb(235, 235, 235);
    color: #333;
    margin: 50px;
    min-height: 250px;
  }

  input, option, textarea{
    color: #333;
  }

  select{
    color: #777;
  }

  .container-title{
    text-align: center;
    font-size: 2.2rem;
    margin-bottom: 50px;
  }

  input::placeholder{
    color: #777;
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
