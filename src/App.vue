<template>
  
  <div id="appVue">
    <h1>Esta es la aplicación SPA</h1>

    <!-- 3. utilizar-->
    <!--
      <PropiedadesComputadas></PropiedadesComputadas>
    -->
    <PropiedadesComputadas 
        titulo = "Este titulo viene del padre"
        parrafo = "Este parrafo viene del padre"
        v-on:eventoEmitidoPorElHijo = "procesarEventoHijo"
    />

    <hr>
    <p> Esto sigue siendo el componente padre (SPA)</p>
    <h4>Datos recibidos del hijo</h4>
    <p id="parrafoEvento">{{  datosHijo }}</p>

  </div>

</template>

<script>
// 1. importar
import PropiedadesComputadas from '@/components/PropiedadesComputadas.vue';

export default {
  name: 'App',
  components: {
    //2. Registrar
    PropiedadesComputadas,
  },
  data: function(){
    return{
      datosHijo:'',
    }
  }, 
  methods:{
    procesarEventoHijo: function(datosRecibidos){
      console.log(datosRecibidos);
      this.datosHijo= datosRecibidos;

    },
  },
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}

#appVue{
  background-color: coral;
  color:yellow;
}

#parrafoEvento{
  color:blueviolet;
}
</style>
