<template>
  <div>
    <navbar></navbar>
    <shows @clicked="recibePeli"></shows>
    <peli :mostrar="mostrar" :peli-elegida="peliElegida"></peli>
  </div>
</template>

<script>
import shows from './components/Shows.vue';
import navbar from './components/Navbar.vue';
import peli from './components/Peli.vue';

export default {
  name: 'app',
  components: {
    shows, navbar, peli
  },
  data () {
    return {
      peliElegida: {},
      mostrar: false
    }
  },
  methods:{
    recibePeli: function(valor){
      console.log(valor)
      this.peliElegida = valor;
      this.mostrar = true;
    }
  }

}
</script>

<style lang="css">
body{
  background-color: #eceff1;
}
</style>
