<template>
  <Banner />
  <main class="main-container">
    <h1 class="container-title">Monte seu hambúrguer: </h1>
    <BurgerForm />
  </main>
</template>

<script>
import Banner from "../components/Banner.vue"
import BurgerForm from "../components/BurgerForm.vue"

export default {
  name: 'HomeView',
  components: {
    Banner,
    BurgerForm
  }
}
</script>
