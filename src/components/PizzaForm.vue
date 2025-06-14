<template>
<Message :msg="msg" v-show="msg"/>
  <div class="form-container" @submit="criarPizza">
    <form class="pizza-form" action="">
      <label for="nome" class="form-label">Nome do cliente:</label>
      <input
        type="text"
        name="nome"
        id="nome"
        v-model="nome"
        placeholder="Digite o seu nome"
      />

      <label for="massa" class="form-label">Escolha a massa:</label>
      <select name="massa" id="massa" v-model="massa">
        <option value="">Selecione o sabor da pizza</option>
        <option v-for="massa in massas" :key="massa.id" :value="massa.tipo">
          {{ massa.tipo }}
        </option>
      </select>

      <label for="sabor" class="form-label"
        >Escolha o sabor da sua pizza:</label
      >
      <label for="sabor">Escolha o sabor da sua pizza:</label>
      <select name="sabor" id="sabor" v-model="sabor">
        <option value="">Selecione o sabor da pizza</option>
        <option v-for="sabor in sabores" :key="sabor.id" :value="sabor.tipo">
          {{ sabor.tipo }}
        </option>
      </select>

      <label for="opcionais">Selecione os opcionais</label>
      <div
        class="checkbox-container"
        v-for="opcional in opcionaisdata"
        :key="opcional.id"
      >
        <input
          type="checkbox"
          name="opcionais"
          v-model="opcionais"
          :value="opcional.tipo"
        />
        <span> {{ opcional.tipo }} </span>
      </div>

      <input type="submit" value="Criar minha pizza!" class="submit-btn" />
    </form>
  </div>
</template>

<script>
import Message from '../components/Message.vue'
export default {
  name: "PizzaForm",
  components: {
    Message
  },
  data() {
    return {
      massas: null,
      sabores: null,
      opcionaisdata: null,
      nome: null,
      massa: null,
      sabor: null,
      opcionais: [],
      msg: null,
    };
  },
  methods: {
    async getIngredientes() {
      const req = await fetch("http://localhost:3000/ingredientes");
      const data = await req.json();

      this.massas = data.massas;
      this.sabores = data.sabores;
      this.opcionaisdata = data.opcionais;
    },
    async criarPizza(e) {
      e.preventDefault();
      const data = {
        nome: this.nome,
        massa: this.massa,
        sabor: this.sabor,
        opcionais: Array.from(this.opcionais),
        status: "Solicitado",
      };
      console.log(data);

      const dataJson = JSON.stringify(data);

      const req = await fetch("http://localhost:3000/pizzas", {
        method: "POST",
        headers: { "Content-type": "application/json" },
        body: dataJson,
      });

      const res = await req.json();
      console.log(res);

      //Tratar mensagens de retorno
      this.msg="Pedido realizado com sucesso!"

      setTimeout(() => this.msg = '', 3000)

      //Limpar campos do formulário
      this.nome = ""
      this.massa = ""
      this.sabor = ""
      this.opcionais = []
    },
  },
  mounted() {
    this.getIngredientes();
  },
};
</script>

<style scoped>
.form-container {
  display: flex;
  justify-content: center;
  align-items: center;
}

.pizza-form {
  text-align: left;
  padding: 40px;
  width: 50%;
}

.pizza-form input[type="text"],
.pizza-form select {
  width: 100%;
  padding: 8px 10px;
  margin-top: 5px;
  border: 1px solid #444;
  border-radius: 4px;
}

.submit-btn {
  margin-top: 20px;
  width: 100%;
  padding: 10px;
  background-color: #ffcc00;
  font-weight: bold;
  cursor: pointer;
}

.form-label {
  display: flex;
  align-items: center;
  font-weight: bold;
  margin-top: 15px;
  margin-bottom: 5px;
  position: relative;
  padding-left: 12px;
  border-left: 6px solid #ffcc00;
}
</style>
