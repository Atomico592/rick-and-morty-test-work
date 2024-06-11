<template>
<div>
  <h1>Rick and Morty Character List</h1>

  <div v-if="charactersData.length">
    <Card v-for="character in charactersData" :key="charactersData.id" :character="character"  :characters-data="character"/>
  </div>
</div>
</template>
<script>
import { ref, watch, onMounted } from 'vue';
import axios from 'axios';
import Card from "@/components/Card.vue";

export default {
 components: {Card},

setup() {
  const charactersData = ref([]);
  const loading = ref(false);
  const error = ref(null);

const fetchCharactertsList = async () => {
    loading.value = true;
    error.value = null;
    try {
      const { data } = await axios('https://rickandmortyapi.com/api/character')

      if(data) {
        charactersData.value = data.results;
      }
      loading.value = false;

    } catch (e) {
      loading.value = false;
      error.value = "An error occurred while loading data";
    }
};

watch(fetchCharactertsList, {immediate: true})

  return {
   charactersData,
    loading,
    error
  };
 }
};

</script>