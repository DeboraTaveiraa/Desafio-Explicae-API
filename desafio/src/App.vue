<template>
  <table>
    <thead>
      <tr>
        <th>DADOS PESSOAIS</th>
      </tr>
    </thead>
    
    <tr>
      <th>NOME:</th>
      <th>SEXO:</th>
    </tr>
    <tr>
      <td>{{ fullName }}</td>
      <td>{{ gender }}</td>
    </tr>

    <thead>
      <tr>
          <th>CONTATOS</th>
      </tr>
    </thead>
    <tr>
      <th>CELULAR:</th>
      <th>TELEFONE:</th>
      <th>E-MAIL:</th>
    </tr>
    <tr v-for="contato in contatos" :key="contato.id">
      <td>{{ contato.cell }}</td>
      <td>{{ contato.phone }}</td>
      <td>{{ contato.email }}</td>
    </tr>
  </table>
</template>

<script>
import Resultado from './services/datasAPI'

export default {

  data(){
    return {
      firstName: '',
      lastName: '',
      gender: '',

      contatos: [
        {cell: '',
        phone: '',
        email: ''
        }
      ]
       
    }
  },

  mounted(){
    Resultado.listar().then(resposta => {
      console.log(resposta.data.results[0])
      this.firstName =  resposta.data.results[0].name.first 
      this.lastName = resposta.data.results[0].name.last 
      this.gender = resposta.data.results[0].gender

      this.contatos[0].cell = resposta.data.results[0].cell
      this.contatos[0].phone = resposta.data.results[0].phone 
      this.contatos[0].email = resposta.data.results[0].email
    })
  },

  computed: {
    fullName() {
      return `${this.firstName} ${this.lastName}`
    }
  }
}

</script>

<style>
  thead{
    background-color: #ff00ff; 
    color: #fff;}
</style>
