<template>
    <div class="border">
        <h1>Cena {{ indiceRey+1 }} con el rey godo {{ productos[indiceRey].nombre }}</h1>
        <h3>Precio: {{ productos[indiceRey].precio }}</h3>
        <div v-if="productos[indiceRey].finDeSemana" class="finDeSemana dias">(Solo fines de semana)</div>
        <div v-else class="todosLosDias dias">(De lunes a domingo)</div>
        <div v-if="productos[indiceRey].precio < 100" class="oferta">
          <span>Ahora un 10% dto: {{ nuevoPrecio }}</span>
          <img :src="oferta" alt="Oferta" />
        </div>
        <img :src="imagenRey" alt="Rey" /><br/>
        <button @click="siguienteRey">Siguiente ({{ indiceRey+1 }}/{{ productos.length }})</button>
    </div>
</template>


<script setup>
  import { computed, ref } from 'vue';
  import { productos } from './datos';

  const indiceRey = ref(0);
  const nuevoPrecio = computed(() => productos[indiceRey.value].precio * 0.9);
  const imagenRey = computed(() => `https://www.html6.es/img/rey_${productos[indiceRey.value].nombre}.png`);

  const oferta = "oferta.jpg";
  const siguienteRey = computed(() => {
    // Código para cambiar el rey y mostrar el siguiente
    if (indiceRey.value < productos.length - 1) {
      indiceRey.value++;
    } else {
      indiceRey.value = 0;
    }
  });

</script>

<style scoped>
.img {
  display: block;
}
 .border {
   border: 1px solid black;
   border-radius: 10px;
   width: 100%;
   height: auto;
   text-align: center;
   padding-bottom: 1em;
 }
 .todosLosDias {
   background-color: green;
 }
  .finDeSemana {
    background-color: red;
  }
  .dias {
    /* Rounded borders */
    border-radius: 5px;
    color: white;
    padding:4px 17px;
    font-size: 0.9em;
    margin: 5px 0 10px;
    display: inline-block;
  }
  .oferta img {
    width: 50px;
  }
</style>