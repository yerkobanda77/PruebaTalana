<template>
  <div class="home">
    <Encabezado :carroCompras="carroCompras" :totalCarro="totalCarro"/>
    <div>
      <b-row>
        <b-col cols="2">
          <Categorias v-on:categoria="onSeleccionoCategoria"/>
        </b-col>
        <b-col cols="10">
          <Productos :categoria="categoriaSeleccionada" :productos="productos" v-on:producto="onAgregarCarro"/>
        </b-col>
      </b-row>
    </div>
    
  </div>
</template>

<script>
// @ is an alias to /src
import Encabezado from '@/components/Encabezado.vue'
import Categorias from '@/components/Categorias.vue'
import Productos from '@/components/Productos.vue'
const axios = require('axios');
export default {
  name: 'Home',
  components: {
    Encabezado,
    Categorias,
    Productos
  },
 data(){
      return {
            categoriaSeleccionada: null,
            productos:[],
            carroCompras:[]
      }
  },
  mounted() {
      if (localStorage.getItem('carro')) {
        this.carroCompras = JSON.parse(localStorage.getItem('carro'));
      }
  },
  methods: {
      onSeleccionoCategoria(categoria) {
        //console.log('onSeleccionoCategoria',categoria);
        this.categoriaSeleccionada = categoria;
        axios
          .get('http://sva.talana.com:8000/api/product/')
          .then(response => {
            this.productos = [];
            response.data.forEach(prod => {
              //Esto no es lo ideal, pero considerando que los productos no vienen filtrado por categoria
              if(prod.category.id === this.categoriaSeleccionada.id){
                prod.cantidadSeleccionada = 0;
                this.productos.push(prod);
              }
            });
          //console.log('products',response.data)
          })
      },
      onAgregarCarro(producto) {
        console.log('onAgregarCarro',producto)
        var carro = [];
        if (localStorage.getItem('carro')) {
          carro = JSON.parse(localStorage.getItem('carro'));
        }
        carro.push(producto);
        const parsed = JSON.stringify(carro);
        localStorage.setItem('carro', parsed);    
        this.carroCompras = carro;  
      }
   },
    computed:{
      totalCarro(){
        return this.carroCompras.length;
      }
    }
}
</script>
