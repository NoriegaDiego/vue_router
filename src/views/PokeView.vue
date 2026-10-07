<script setup>
import {useRoute, useRouter} from 'vue-router'
import {useGetData} from '@/composables/getData'
import {useFavoritosStore} from '@/store/favoritos'


const route = useRoute();
const router = useRouter();
const useFavoritos = useFavoritosStore();

const {add, findPoke}= useFavoritos;

const {getData, data, loading, error} = useGetData();

const back = () => {
    router.push('/pokemons')
}
// const getData = async () => {
//     try{
// const {data} = await axios.get(`https://pokeapi.co/api/v2/pokemon/${route.params.name}`);
// console.log(data);
// poke.value = data;
//     } catch (error){
//         console.log(error)
//         poke.value = null;
//     }
    
// }
getData(`https://pokeapi.co/api/v2/pokemon/${route.params.name}`);
</script>

<template>
    <p v-if="loading">Cargando informacion...</p>
    <div class="alert alert-danger mt-2" v-if="error">{{ error }}</div>
    <div v-if="data">
    <img :src="data.sprites?.front_default">
    <h1>Poke name: {{ $route.params.name }}</h1>
    <button :disabled="findPoke(data.name)" class="btn btn-outline-primary mb-2" @click="add(data)">Agregar a favoritos</button>
    </div>
    <h1 v-else>No existe el pokemon</h1>
    <button class="btn btn-outline-primary" @click="back">Back</button>
</template>