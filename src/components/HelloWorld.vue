<template>
    <div></div>
</template>

<script>
import ListaPalabras from '/src/data/palabras.json'
export default {
  name: 'HelloWorld',
  data: function(){
    return {
      palabras: ListaPalabras
    }
  }

}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
</style>
