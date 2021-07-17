<template>
  <div id="app">
    <Pcard :img="dados.avatar_url" :nome="dados.login">
    <hr><p>projetos:</p><br>
    <p v-for="repo in repos" :key="repo.id" >
<span class="lang">
{{repo.language}}<br>
</span>
      {{repo.name}}<br>{{repo.description}}<br>
      <a :href="repo.html_url">{{ repo.html_url }}</a>
      </p>
    </Pcard>
    <p>{{ erro }}</p>
  </div>



</template>

<script>
import Api from'./services/api'
import Pcard from './components/Pcard.vue'

export default {
data(){
  return{
    dados:[], //array de dados da busca
    user: 'emerson-douglas', //nome do usuario que você deseja buscar
    erro:'',
    repos:[],

  }
},

  name: 'App',
    components: {
    Pcard
  },

  created(){
    //quando a tela é carregada realiza a busca na API
    Api.get("users/"+this.user)
    .then(res =>{
    this.dados = res.data
    Api.get(this.dados.repos_url) //pega a lista de repositorios
    .then(r=>this.repos = r.data,
    err=>console.log(err))
    },
    ()=>this.erro="ocorreu um erro ao carregar os dados,tente novamente mais tarde"
  )}
}
</script>

<style>
#app {
  padding: 40px;
  display: flex 0;
  align-content: center;
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: white;
  margin-top: -20px;
  height:100%;
  width: auto;
  background:#2c3e50 ;
}
a{color:white}
.lang{
  background: gray;
  color: black;
}
body {
  background: #2c3e50;
}
</style>
