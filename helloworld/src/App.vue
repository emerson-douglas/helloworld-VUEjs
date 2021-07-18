<template>
  <div id="app">
    <input  name="busca" 
    id="busca" autocomplete="off" v-model="busca">
    <button @click="buscar">buscar</button>
    <Pcard :img="dados.avatar_url" :nome="dados.login" v-show="!imgerro"/>

    <!--componente <erro> !-->
  <center>
    <p v-for="repo in repos" :key="repo.id" v-show="!imgerro">
    <Repo :nome="repo.name" :desc="repo.description" :url="repo.html_url" :lang="repo.language"/>
      </p>
  </center>

    <p>{{ erro }}</p>
    <img v-show="imgerro" 
    src="./assets/404.png"/>
    </div>



</template>

<script>
import Api from'./services/api'
import Pcard from './components/Pcard.vue'
import Repo from './components/Projetos.vue'

export default {
data(){
  return{
    dados:[], //array de dados da busca
    busca: '', //nome do usuario que você deseja buscar
    erro:'',
    imgerro: false,
    repos:[],

  }
},

  name: 'App',
    components: {
    Pcard,
    Repo,
  },

  created(){
    this.buscar()

},
  methods:{
    buscar(){
      //quando a tela é carregada realiza a busca na API
    Api.get("users/"+this.busca)
    .then(res =>{
      this.erro=''
      this.imgerro=false
    this.dados = res.data
    Api.get(this.dados.repos_url) //pega a lista de repositorios
    .then(r=>this.repos = r.data,
    err=>console.log(err))
    },
    ()=>{
      this.dados=[];this.repos=[]
      this.erro=`ocorreu um erro ao realizar a busca, rocure por um outro usuario`
      this.imgerro = true}
  )}
    }

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
body {
  background: #2c3e50;
}
</style>
