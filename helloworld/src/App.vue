<template>
  <div id="app">

    <p>{{ dados.login }}</p>
    <img :src="dados.avatar_url" :alt="dados.login">
    <hr><p>projetos:</p><br>
    <p v-for="repo in repos" :key="repo.id" >
      ...{{repo.name}}..<br>{{ repo.html_url }}
      </p>

  </div>



</template>

<script>
import api from'./services/api'

export default {
data(){
  return{
    dados:[], //array de dados da busca
    user: 'emerson-douglas', //nome do usuario que você deseja buscar
    repos:[],

  }
},

  name: 'App',
  components: {},

  created(){
    //quando a tela é carregada realiza a busca na API
    api.get("users/"+this.user)
    .then(res =>
    {this.dados = res.data
    api.get(this.dados.repos_url) //pega a lista de repositorios
    .then(r=>this.repos = r.data,
    err=>console.log(err))
    },
     err=>console.log("ops! ocorreu um erro" + err)
  )}
}
</script>

<style scoped>
.card{
}
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
