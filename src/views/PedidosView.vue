<template>
  <div class="main-container">
    <h1>Gerenciar Pedidos</h1>
    <DashPedidos />
  </div>
</template>

<script>
import DashPedidos from '../components/DashPedidos.vue'
export default {
  name: "PedidosView",
  components: {
    DashPedidos,
  }
}
</script>