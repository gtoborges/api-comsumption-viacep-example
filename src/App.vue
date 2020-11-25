<template>
  <div id="app">
    <img alt="Vue logo" src="./assets/logo.png" style="margin-right: -80px; margin-bottom: -15px">iacep
    <br>
    <p style="margin-bottom: 0">Digite apenas os 8 dígitos do cep para buscar</p>
    <input type=text v-model="cep" style="margin-top: 1rem; text-align: center"><button @click="buscarCep()">Buscar</button>
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
      let digitos = this.cep.split('')
      if(digitos.length != 8) {
        console.log(isNaN(2))
        alert('Não foram encontrados exatamente 8 dígitos')
        this.enderecoEncontrado = {}
        return
      }
      if(digitos.find(n => isNaN(Number(n)) )) {
        alert('Algum dos 8 dígitos não é um número. Apenas números permitidos')
        this.enderecoEncontrado = {}
        return
      }
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
