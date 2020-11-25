<template>
  <div class="hello">
    <h1>{{ msg }}</h1>
    <h3>CEP</h3>
    <p>{{ enderecoEncontrado.cep }}</p>
    <h3>Logradouro</h3>
    <p>{{ enderecoEncontrado.logradouro}}</p>
    <h3>Bairro</h3>
    <p>{{ enderecoEncontrado.bairro}}</p>
    <h3>Cidade</h3>
    <p>{{ enderecoEncontrado.localidade}}</p>
    <h3>Unidade Federativa</h3>
    <p>{{ enderecoEncontrado.uf}}</p>
  </div>
  
</template>

<script>
export default {
  name: 'Endereco',
  props: {
    msg: String,
    enderecoEncontrado: Object
  }
}
</script>
<style scoped>
h3 {
  margin: auto;
}
p {
  margin: .5rem 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
</style>
