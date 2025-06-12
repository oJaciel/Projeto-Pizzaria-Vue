<template>
  <div id="pizza-table">
    <div>
      <div id="pizza-table_heading">
        <div class="order-id">#</div>
        <div>Cliente</div>
        <div>Massa</div>
        <div>Sabor</div>
        <div>Opcionais</div>
        <div>Ações</div>
      </div>
      <div id="pizza-table-rows">
        <div class="pizza-table-row" v-for="pizza in pizzas" :key="pizza.id">
          <div class="order-number">{{ pizza.id }}</div>
          <div>{{ pizza.nome }}</div>
          <div>{{ pizza.massa }}</div>
          <div>{{ pizza.sabor }}</div>
          <div>
            <ul v-for="(opcinal, index) in pizza.opcionais" :key="index">
              <li>{{ opcional }}</li>
            </ul>
          </div>
          <div>
            <select
              name="status"
              class="status"
              @change="updatePizza($event, pizza.id)"
            >
              <option
                value="s.tipo"
                v-for="s in status"
                :key="s.id"
                :selected="pizza.status == s.tipo"
              >
                {{ s.tipo }}
              </option>
            </select>
            <button @click="deletePizza(pizza.id)">Cancelar</button>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "DashPedidos",
  data() {
    return {
      pizzas: null,
      pizza_id: null,
      status: [],
      msg: null,
    };
  },
  methods: {
    async getPedidos() {
      const req = await fetch("http://localhost:3000/pizzas");
      const data = await req.json();
      this.pizzas = data;

      this.getStatus();
    },
    async getStatus() {
      const req = await fetch("http://localhost:3000/status");
      const data = await req.json();
      this.status = data;
    },
    async deletePizza(id) {
      const req = await fetch(`http://localhost:3000/pizzas/${id}`, {
        method: "DELETE",
      });
      const res = await req.json();
      this.getPedidos();
    },
    async updatePizza(event, id) {
      const option = event.target.value;
      const dataJson = JSON.stringify({ status: option });

      const req = await fetch(`http://localhost:3000/pizzas/${id}`, {
        method: "PATCH",
        headers: { "Content-Type": "application/json" },
        body: dataJson,
      });

      const res = await req.json()
      console.log(res)
    },
  },
  mounted() {
    this.getPedidos();
  },
};
</script>

<style scoped>
</style>