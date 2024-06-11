<template>
<div>
  <h1>Rick and Morty Character List</h1>
</div>
</template>
<script>
import { ref, watch, onMounted } from 'vue';
import axios from 'axios';

export default {
 components: {},

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