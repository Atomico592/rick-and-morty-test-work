<template>
<div>
  <div class="title">
  <h1>Rick and Morty Character List</h1>
  </div>

  <div class="page-navigation">
    <h3>Page navigation</h3>
  <Filter :filters="filters" @apply-filters="filterHandler"/>
  <Pagination :totalPage="totalPage" :currentPage="currentPage" @page-changed="changePage" />
  </div>

  <div v-if="loading" class="backdrop" >
  <div  class="preloader">
    <img :src="preloader" alt="Loading" class="loading-image"/>
  </div>
  </div>
  <div v-if="error">{{error}}</div>


  <div v-if="charactersData.length" class="card-wrapper">
    <Card v-for="character in charactersData" :key="charactersData.id" :character="character"  :characters-data="character"/>
  </div>
</div>
</template>
<script>
import { ref, watch } from 'vue';
import axios from 'axios';
import Card from "@/components/Card.vue";
import Pagination from "@/components/Pagination.vue";
import Filter from "@/components/Filter.vue";
import preloader from "./assets/preloader.gif";

export default {
 components: {Filter, Card, Pagination},

setup() {
  const charactersData = ref([]);
  const loading = ref(false);
  const error = ref(null);
  const currentPage = ref(1);
  const totalPage = ref (1);
  const filters = ref({
    name: "",
    status : ""
  })


const fetchCharactertsList = async () => {
    loading.value = true;
    error.value = null;
    try {
      const { data } = await axios('https://rickandmortyapi.com/api/character', {
        params : {
          page: currentPage.value,
          name: filters.value.name,
          status: filters.value.status
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

const filterHandler = () => {
    currentPage.value = 1;
    fetchCharactertsList();
}

watch([currentPage] ,fetchCharactertsList, {immediate: true})

  return {
   charactersData,
    loading,
    error,
    preloader,
    currentPage,
    totalPage,
    changePage,
    filters,
    filterHandler
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
.title {
  text-align: center;
  font-size: 50px;
  padding: 50px 0;
  font-weight: bold;
}
.card-wrapper {
  background-color: rgb(39, 43, 51);
  padding: 15px 2px 2px 2px;
  display: flex;
  flex-wrap: wrap;
  width: 100%;
}
.page-navigation {
  padding: 25px;
  background-color: antiquewhite;
}
</style>