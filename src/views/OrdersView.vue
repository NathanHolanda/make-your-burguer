<template>
  <main class="main-container">
    <h1 class="container-title">Pedidos</h1>
    <OrdersTable />
  </main>
</template>

<script>
import OrdersTable from "../components/OrdersTable.vue"

export default {
  components: {
    OrdersTable
  }
}
</script>