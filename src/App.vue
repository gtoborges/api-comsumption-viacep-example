<template>
  <div id="app">
    <img alt="Vue logo" src="./assets/logo.png">iacep
    <input type=text v-model="cep"><button @click="buscarCep()">buscar</button>
    <Endereco msg="Endereço encontrado: " :enderecoEncontrado="enderecoEncontrado" v-if="Object.keys(enderecoEncontrado).length"/>
  </div>
</template>

<script>
import Endereco from './components/Endereco.vue'

export default {
  name: 'App',
  components: {
    Endereco
  },
  data () {
    return {
      cep: '',
      enderecoEncontrado: {}
    }
  },
  created() {
    this.cep = '74690900'
    this.buscarCep()
  },
  methods: {
    async buscarCep() {
      try {
        let response = await fetch(`https://viacep.com.br/ws/${this.cep}/json/`)
        let data = await response.json()
        let {erro, cep, logradouro, bairro, localidade, uf} = data
        if(erro) throw 'Erro ao tentar buscar pelo cep. Tente novamente e verifique se o cep informado está correto!'
        else {
          this.enderecoEncontrado = {cep, logradouro, bairro, localidade, uf}
        }
      } catch (e) {
        this.enderecoEncontrado = {}
        alert(e)
      }
    }
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
