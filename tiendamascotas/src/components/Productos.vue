<template>
  <div>
    <div v-if="categoria === null">Seleccione una Categoría</div>
    <div v-if="categoria != null">
        <h2>{{categoria.name}}</h2>
        <div v-if="productos.length === 0">SIN PRODUCTOS</div>
        <div v-if="productos.length > 0">
            <b-row>
                <b-col cols="3" v-for="producto of productos" v-bind:key="producto.id">
                    <b-img  :src="producto.photo" thumbnail fluid :alt="producto.abstract" style="width:90%; height: 70%"></b-img>
                    <strong>{{producto.name}}</strong>
                    <p>Precio: ${{producto.price}}</p>
                    <b-row>
                        <b-col cols="2"></b-col>
                        <b-col cols="7">
                            <b-input-group class="mt-3">
                                <b-button variant="danger" @click="producto.cantidadSeleccionada--">
                                    <b-icon icon="dash" aria-hidden="true"></b-icon>
                                </b-button>
                                <b-form-input v-model="producto.cantidadSeleccionada" type="number" readonly style="text-alignt:center"></b-form-input>
                                <b-button variant="success" @click="producto.cantidadSeleccionada++">
                                    <b-icon icon="plus" aria-hidden="true" ></b-icon>
                                </b-button>
                                <b-input-group-append>
                                <b-button variant="primary" @click="agregar(producto)">
                                    <b-icon icon="cart-check" aria-hidden="true"></b-icon>
                                </b-button>
                                </b-input-group-append>
                            </b-input-group>
                        </b-col>
                    </b-row>
                </b-col>
            </b-row>
            <!-- {{productos}} -->
        </div>
        
    </div>
  </div>
</template>

<script>
export default {
  name: 'Productos',
  props: ['categoria','productos'],
   methods: {
    agregar(prod) {
      // asegurarse que el usuario efectivamente ha escrito algo
      if (prod.cantidadSeleccionada === 0) {
        return;
      }
       this.$emit('producto', prod);
    }
    
  }
}
</script>