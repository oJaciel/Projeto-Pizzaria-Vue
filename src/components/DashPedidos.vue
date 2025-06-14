<template>
  <Message :msg="msg" v-show="msg" />
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
            <ul>
              <li v-for="(opcional, index) in pizza.opcionais" :key="index">
                {{ opcional }}
              </li>
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
import Message from "../components/Message.vue";
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
  components: {
    Message,
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

      //Mensagem de exclusão
      this.msg = "Pedido removido com sucesso!";

      setTimeout(() => (this.msg = ""), 3000);
    },
    async updatePizza(event, id) {
      const option = event.target.value;
      const dataJson = JSON.stringify({ status: option });

      const req = await fetch(`http://localhost:3000/pizzas/${id}`, {
        method: "PATCH",
        headers: { "Content-Type": "application/json" },
        body: dataJson,
      });

      const res = await req.json();
      console.log(res);
    },
  },
  mounted() {
    this.getPedidos();
  },
};
</script>

<style scoped>
#pizza-table {
  margin: 2rem auto;
  max-width: 1000px;
  background: #fff;
  border-radius: 12px;
}

#pizza-table_heading {
  display: grid;
  grid-template-columns: 50px 1fr 1fr 1fr 2fr 1fr;
  background-color: #f5f5f5;
  font-weight: bold;
  padding: 12px 16px;
  border-bottom: 2px solid #ddd;
}

#pizza-table-rows {
  display: flex;
  flex-direction: column;
  gap: 8px;
  padding: 12px 0;
}

.pizza-table-row {
  display: grid;
  grid-template-columns: 50px 1fr 1fr 1fr 2fr 1fr;
  align-items: center;
  background-color: #fafafa;
  padding: 10px 16px;
  border-radius: 8px;
  border-left: 6px solid #ffcc00;
}

.pizza-table-row:hover {
  background-color: #f0f0f0;
}

.order-id,
.order-number {
  font-weight: bold;
  color: #444;
  text-align: center;
}

.status {
  padding: 4px 8px;
  border-radius: 6px;
  font-size: 0.9rem;
  margin-bottom: 6px;
}

button {
  padding: 4px 8px;
  background-color: #e53935;
  color: #fff;
  border-radius: 6px;
}

button:hover {
  background-color: #c62828;
}
</style>
