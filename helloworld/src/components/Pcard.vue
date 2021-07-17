<template>
<div class="Pcard">

    <h1>{{ nome }}</h1><br>
    <img :src="img" :alt="nome"/>

    <slot>
    </slot>

</div>
    
</template>
<script>
export default {
  name: 'HelloWorld',
  props: {
    img: String,
    nome: String,
  }
}
</script>

<style scoped>
.Pcard{
    width: 100%;
    height: 100%;

}
img{
    width: 200px;
    border-radius: 400px;
    border: 5px solid black;
}

</style>