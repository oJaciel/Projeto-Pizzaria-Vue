<template>
  <div class="form-container">
    <form class="pizza-form" action="">
      <label for="client_name" class="form-label">Nome do cliente:</label>
      <input
        type="text"
        name="client_name"
        id="client_name"
        placeholder="Digite o seu nome"
      />

      <label for="massa" class="form-label">Escolha a massa:</label>
      <select name="massa" id="massa"></select>

      <label for="sabor" class="form-label"
        >Escolha o sabor da sua pizza:</label
      >
      <select name="sabor" id="sabor"></select>

      <label for="opcionais" class="form-label">Selecione os opcionais:</label>
      <div class="checkbox-wrapper">
        <input type="checkbox" name="opcionais" id="opcionais" />
        <label for="opcionais">Borda com catupiry</label>
      </div>

      <input type="submit" value="Criar minha pizza!" class="submit-btn" />
    </form>
  </div>
</template>

<script>
export default {
  name: "PizzaForm",
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
  border: 1px solid #ccc;
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
