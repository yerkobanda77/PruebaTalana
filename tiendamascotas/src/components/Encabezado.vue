<template>
    <div>
    <b-navbar toggleable="lg" type="dark" variant="info">
        <b-navbar-brand :to="{name:'Home'}" style="width: 5%">
        <img src="../assets/logo2.png" width="50%">
        </b-navbar-brand>

        <b-navbar-toggle target="nav-collapse"></b-navbar-toggle>

        <b-collapse id="nav-collapse" is-nav>
        <b-navbar-nav>
            Bienvenido a la tienda de Mascotas
            <!-- <b-nav-item :to="{name:'Home'}" exact>Link</b-nav-item>
            <b-nav-item :to="{name:'About'}">Disabled</b-nav-item> -->
        </b-navbar-nav>

        <!-- Right aligned nav items -->
        <b-navbar-nav class="ml-auto">
            <b-nav-form>
            <b-form-input size="lg" class="mr-sm-2" placeholder="Buscador de Productos"></b-form-input>
            <b-button size="sm" class="my-2 my-sm-0" type="submit">Buscar</b-button>
            </b-nav-form>
            <b-nav-form>
            <b-button variant="primary" size="sm" class="my-2 my-sm-0" v-b-modal.modal1>
                <b-icon icon="cart-check" aria-hidden="true"></b-icon><b-badge pill variant="danger">{{totalCarro}}</b-badge>
            </b-button>
            </b-nav-form>
        </b-navbar-nav>
        </b-collapse>
  </b-navbar>
  <b-modal id="modal1" title="Resumen de Productos"  hide-footer>
    <div v-if="totalCarro === 0">SIN PRODUCTOS</div>
    <div v-if="totalCarro > 0">
        <b-row>
            <b-col cols="3" v-for="producto of carroCompras" v-bind:key="producto.id">
                <b-img  :src="producto.photo" thumbnail fluid :alt="producto.abstract" style="width:90%; height: 70%"></b-img>
                <strong>{{producto.name}}</strong>
                <p>Precio: ${{producto.price}}</p>
                
            </b-col>
        </b-row>
    </div>
    <b-button style="margin-top:30px" class="mt-3" block @click="$bvModal.hide('modal1')">CERRAR</b-button>
  </b-modal>
  </div>
</template>

<script>
  export default {
    name: 'Encabezado',
    props: ['carroCompras','totalCarro']    
  }
</script>