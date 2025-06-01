<template>
    <div>
        <form action="">
            <label for="client_name">Nome do cliente:</label>
            <br>
            <input type="text" name="client_name" id="client_name" placeholder="Digite o seu nome">
            <br>
            <label for="massa">Escolha a massa:</label>
            <br>
            <select name="massa" id="massa" disabled="disabled"></select>
            <br>
            <label for="sabor">Escolha o sabor da sua pizza:</label>
            <br>
            <select name="sabor" id="sabor" disabled="disabled"></select>
            <br>
            <label for="opcionais">Selecione os opcionais:</label>
            <br>
            <input type="checkbox" name="opcionais" id="opcionais" placeholder="Borda com catupiry">
            <br>
            <input type="submit" value="Criar minha pizza!">
        </form>
    </div>
</template>

<script>
export default {
    name: "PizzaForm",
}
</script>

<style scoped>

</style>