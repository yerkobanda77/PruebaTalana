<template>
  <div>
    <h2>Categorías:</h2>
    <ul>
        <li v-for="categoria of categorias" v-bind:key="categoria.id">
            <button @click="seleccionarCategoria(categoria)">{{categoria.name}}</button>            
        </li>
    </ul>
  </div>
</template>

<script>
const axios = require('axios');
export default {
  name: 'Categorias',
  data(){
      return {
            categorias: []
      }
  },
  mounted () {
    axios
      .get('http://sva.talana.com:8000/api/product-category/')
      .then(response => {this.categorias = response.data;})
  },
  methods: {
      seleccionarCategoria(parametros) {
         this.$emit('categoria', parametros);
      }
   }
}
</script>