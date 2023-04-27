<script setup>
import {ref, computed } from 'vue'
    const name = "Vue 3";
    const contador = ref(0)
    
    const incrementar = ()=>{
      contador.value++
    }
    const desincrementar = ()=>{
      contador.value--
    }
    const reiniciar = ()=>{
      contador.value=0
    }
    const colorContador= computed(()=>{
      if(contador.value === 0){
        return 'zero'
      }
      if(contador.value > 0){
        return 'positivo'
      }
      if(contador.value < 0){
        return 'negativo'
      }
    })

    const favoritos= ref([])

    const addFavoritos = () =>{
      favoritos.value.push(contador.value)
    }

    const validarItemfav = computed ( () => {
      const buscarItem = favoritos.value.find((num) => num === contador.value);
      if(buscarItem === 0) return true
      return buscarItem ? true : false;
    })
</script>
<template>
   <div class="container text-center mt-3">
    <h1>hola {{ name.toUpperCase()}}</h1>
    <h2 :class="colorContador" >
      {{ contador }}
    </h2>
    <div class="btn-group">
    <button @click="incrementar" class="btn btn-success">INCREMENTAR</button>
    <button @click="desincrementar" class="btn btn-danger">DESINCREMENTAR</button>
    <button @click="reiniciar" class="btn btn-secondary">REINICIAR</button>
    <button @click="addFavoritos" class="btn btn-primary" :disabled="validarItemfav">FAVORITO</button>
    
      </div>
    <h2 v-for="item in favoritos">
      <ul class="list-group mt-4">
        <li class="list-group-item">{{ item }}</li>  
      </ul>
    </h2>
    </div>
</template>
<style>
  h1{
    color: red;
  }
  .positivo{
    color: green;
  }
  .negativo{
    color: red;
  }
  .zero{
    color: blue;
  }
  </style>