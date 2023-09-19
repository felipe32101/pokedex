<template>
<div id="todo">
  <div id="part1" :style="c==true ? 'display:flex': 'display: none'">
    <div id="part1_1">
      <h1 id="num">#{{ num }}</h1>
      <h1 id="nombre">{{ nombre }}</h1>
      <div>
        <h4></h4>
        <h4></h4>
      </div>
      <div style="display: flex; flex-direction: row; justify-content: space-between; width: 70%;">
        <h2>Peso</h2>
        <h2>Altura</h2>
      </div>
      <div style="display: flex; flex-direction: row; justify-content: space-between; width: 70%;">
        <h4>{{ peso }}</h4>
        <h4>{{ altura }}</h4>
      </div>
    </div>
    <div id="part1_2">
      <img :src="img" alt="">
    </div>
  </div>
  <div id="part2" :style="c==true ? 'display:flex': 'display: none'">
    <div style="width: 80%; display: flex; width: 20%; padding-left: 150px; align-items: center; justify-content: center;">
      <div class="stats">
        <h1>HP</h1>
        <h1>{{ hp }}</h1>
      </div>
    </div>
  </div>
  <button @click="obtenerUrlPokemon()">Peticion</button>
</div>
</template>

<script setup>
import axios from "axios"
import {ref} from "vue"

const c = ref(false)

const img = ref("")
const num = ref("")
const nombre = ref("")
const altura = ref("")
const peso = ref("")
const hp = ref("")

async function obtenerUrlPokemon(){
  c.value = true
  let r = await axios.get("https://pokeapi.co/api/v2/pokemon/555/")
  img.value = r.data.sprites.other['official-artwork'].front_default
  num.value = r.data.id
  nombre.value = r.data.name
  altura.value = r.data.height
  peso.value = r.data.weight
  hp.value = r.data.stats[0].base_stat
}

</script>

<style scoped>
#todo{
  width: 100%;
  max-height: 100vh;
}

#part1{
  display: flex;
  flex-direction: row;
}

#part1_1{
  width: 50%;
  padding-left: 150px;
}

#num{
  font-size: 200px;
  font-family: fantasy;
  color: rgb(127, 127, 220);
  margin: 0;
}

#nombre{
  font-size: 70px;
  margin: 0;
  font-family: fantasy;
}

#part1_1{
  gap: 50px;
}

#part1_2{
  width: 50%;
}

h4, h3, h2{
  margin: 0;
}

#part2{
  width: 100%;
}

.stats{
  display: flex;
  flex-direction: row;
}
</style>
