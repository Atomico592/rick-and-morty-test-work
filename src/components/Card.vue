<template>
  <div class="card">
    <h2>{{charactersData.name}}</h2>
    <p><span></span> {{charactersData.status}} -  {{charactersData.species}} </p>
    <p>Last known location: {{charactersData.location.name}}</p>
    <img :src="charactersData.image" :alt="charactersData.name">
  </div>
</template>

<script>
  export default {
    props : {
      charactersData : {
        type: Object,
        required: true
      }
    }
  };
</script>

<style scoped>
    .card {
      border: 1px solid #ccc;
      padding: 16px;
      margin: 16px;
      border-radius: 12px;
    }
</style>