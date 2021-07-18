<template>
  <div class="repoCard">
      <span v-show="lang" class="lang"> {{ lang }} </span><br>
      <a :href="url"><p class="titulo">{{nome}}</p></a>
<p/>{{ desc }}<br><br>
  </div>
</template>

<script>
export default {
props:{
    lang: String,
    nome: String,
    desc: String,
    url: String,
}
}
</script>

<style>
.repoCard{
    background: rgb(99, 85, 85);
    width: fit-content;
    padding: 10px;
    border-radius: 10px;
    transition: opacity 2s;  
}.repoCard:hover{
    opacity: 0.2; 
}
.lang{
    background: darkkhaki;
    color: black;
    padding: 2px;
    border-radius: 10px;
}
.titulo{
     font-weight: bold;
}

</style>