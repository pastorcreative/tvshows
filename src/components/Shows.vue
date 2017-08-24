<template lang="html">
  <div>
    <div v-if="pelis == null" class="progress">
      <div class="indeterminate"></div>
    </div>
    <div  v-else class="row">
      <form>
        <div class="input-field">
          <input v-model="busqueda" id="search" type="text" required>
          <label for="search"><i class="material-icons">search</i></label>
        </div>
      </form>
      <template v-for="(peli, index) in busquedaSeries">
        <div class="col s12 m6 l3">
          <div class="card hoverable">
            <div class="card-action center-align ">
            <p><strong> {{ peli.name }} </strong></p>
            </div>
            <div class="card-image">
              <img :src="peli.image.medium">
            </div>
            <div class="card-action center-align">
              <button v-on:click="showModal(peli.id)" type="button" class="waves-effect waves-teal btn-flat pink darken-1 white-text">
                READ MORE
              </button>
            </div>
          </div>
        </div>
      </template>
    </div>
  </div>
</template>


<script>
import axios from 'axios';
import peli from './Peli.vue';
export default {
  data(){
    return{
      pelis: [],
      busqueda:''

    }
  },
  mounted() {
    axios.get('http://api.tvmaze.com/shows')
      .then((respuesta)=>{
        this.pelis = respuesta.data;
      });
  },
  computed: {
    busquedaSeries(){
      return this.pelis.filter((peli) => peli.name.includes(this.busqueda));
    }
  },
  methods: {
    showModal: function(id) {
      this.getPeli(id);
    },
    getPeli: function(id) {

      let url =   `http://api.tvmaze.com/shows/:id`

      axios.get(url.replace(":id", id))
        .then((respuesta) => {
          // return console.log(respuesta)
          this.$emit('clicked', respuesta.data)
        })
        .catch((error)=> {
          console.log(error)
        })
    }
  }
}
</script>

<style lang="css">
.card .card-image .card-title{
  font-size: 16px;
}

</style>
