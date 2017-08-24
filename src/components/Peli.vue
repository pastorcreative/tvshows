<template lang="html">
  <transition name="custom-classes-transition"
    enter-active-class="animated fadeInDown"
    leave-active-class="animated fadeInUp">
    <div v-if="mostrar" class="row">
      <div class="col s12 m6 peli">
        <div class="card large blue-grey lighten-1">
            <button @click="mostrar = false" type="button" class="btn-flat derecha"><i class="material-icons right">close</i></button>
          <div class="card-content white-text">
            <img class="imagen-peli hide-on-small-only" :src="peliElegida.image.medium" align="left" :alt="peliElegida.name">
            <span class="card-title" v-text="peliElegida.name"></span>
            <p v-html="peliElegida.summary"></p>
          </div>
          <div class="card-action">
            <template>
              <div v-for="genre in peliElegida.genres" class="chip pink darken-1 white-text">
                {{ genre }}
              </div>
            </template>
          </div>
        </div>
      </div>
    </div>
  </transition>
</template>

<script>
export default {
  props: ['peliElegida', 'mostrar'],
  data(){
      return{
        show: this.mostrar
      }
    }
  }
</script>

<style lang="css" scoped>
.row .col.m6 {
  position: fixed;
  top: 0;
  left:0;
  right:0;
  bottom:0;
  width:100%;
  z-index:98;
}
.derecha {
  position: absolute;
  z-index: 99;
  top: 0;
  right: 0;
  color: white;
}
.imagen-peli{
  margin-right:25px;
}
.card{
  margin:0;
  height:100vh;
}
</style>
