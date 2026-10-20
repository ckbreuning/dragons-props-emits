<script setup>
import { ref } from "vue";
import dragons from "./assets/js/dragons";
import DragonComp from "./components/DragonComp.vue";

const dragonsList = ref(dragons)

function renameDragon(id, newName) {
  const dragon = dragonsList.value.find(d => d.id === id)
  
  dragon.name = newName
}

function deleteDragon(id) {
  dragonsList.value = dragonsList.value.filter(dragon => dragon.id != id)
}
</script>

<template>

  <header>
    <h1>D&D website</h1>
    <h2>
      Your source for DnD dragons. Providing dragon information since 2021.<br />
      Find info about <span>{{ dragonsList.length }}</span> dragons here.
    </h2>
  </header>
  <main>
        <DragonComp 
        v-for="dragon in dragonsList" 
        :key="dragon.id" 
        :id="dragon.id"
        :name="dragon.name" 
        :image="dragon.img_url" 
        :skills="dragon.Skills" 
        @renameDragon="renameDragon"
        @deleteDragon="deleteDragon"/>
  </main>
</template>

<style scoped>
header {
  text-align: center;
  min-height: 60vh;
  background-image: linear-gradient(rgba(0, 0, 0, 0.3), rgba(0, 0, 0, 0.9)),
    url("@/assets/img/bg_dragon.jpg");
  background-size: cover;
  display: grid;
  place-content: center;
  color: white;
}

h1 {
  font-size: 4rem;
}

span {
  color: crimson;
}

main {
  max-width: 1000px;
  margin: 1rem auto;
  padding: 2rem;
  box-shadow: 0 0 3px 1px rgba(0, 0, 0, 0.3);
  display: grid;
  grid-template-columns: repeat(2, 1fr);
  gap: 1rem;
  border-radius: 6px;
}

@media screen and (max-width: 1050px) {
  main {
    grid-template-columns: 1fr;
    padding: 5rem;
  }
}
</style>
