<template>
<div>
  <h1>Rick and Morty Character List</h1>

  <div v-if="loading" class="backdrop" >
  <div  class="preloader">
    <img :src="preloader" alt="Loading" class="loading-image"/>
  </div>
  </div>
  <div v-if="error">{{error}}</div>

  <Pagination :totalPage="totalPage" :currentPage="currentPage" @page-changed="changePage" />

  <div v-if="charactersData.length">
    <Card v-for="character in charactersData" :key="charactersData.id" :character="character"  :characters-data="character"/>
  </div>
</div>
</template>
<script>
import { ref, watch } from 'vue';
import axios from 'axios';
import Card from "@/components/Card.vue";
import Pagination from "@/components/Pagination.vue";
import preloader from "./assets/preloader.gif";

export default {
 components: {Card, Pagination},

setup() {
  const charactersData = ref([]);
  const loading = ref(false);
  const error = ref(null);
  const currentPage = ref(1);
  const totalPage = ref ({
    name: '',
    status: ''
  });

const fetchCharactertsList = async () => {
    loading.value = true;
    error.value = null;
    try {
      const { data } = await axios('https://rickandmortyapi.com/api/character', {
        params : {
          page: currentPage.value,
        }
      });

      if(data) {
        charactersData.value = data.results;
      }
      loading.value = false;
      totalPage.value = data.info.pages;
    } catch (e) {
      loading.value = false;
      error.value = "An error occurred while loading data";
    }
};

const changePage = (page) => {
  currentPage.value = page;
};

watch([currentPage] ,fetchCharactertsList, {immediate: true})

  return {
   charactersData,
    loading,
    error,
    preloader,
    currentPage,
    totalPage,
    changePage
  };
 }
};

</script>

<style scoped>
.backdrop {
  position: fixed;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  background-color: rgba(0, 0, 0, 0.5);
  display: flex;
  justify-content: center;
  align-items: center;
  z-index: 10;
}
</style>