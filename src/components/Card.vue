<template>
  <div class="card">
    <h2>{{ charactersData.name }}</h2>
    <p><span :class="['status-circle', charactersData.status === 'Alive' ? 'alive' : charactersData.status === 'Dead' ? 'dead' : 'unknown']"></span>
      {{ charactersData.status }} - {{ charactersData.species }} </p>
    <p>Last known location: {{ charactersData.location.name }}</p>
    <img :src="charactersData.image" :alt="charactersData.name" class="card-image">
  </div>
</template>

<script>
export default {
  props: {
    charactersData: {
      type: Object,
      required: true
    }
  },
};
</script>

<style scoped>
.card {
  border: 1px solid #ccc;
  background-color: #fff;
  padding: 16px;
  margin: 16px;
  border-radius: 12px;
  width: 15%;
}

.card-image {
  width: 100%;
  height: auto;
}

.status-circle {
  display: inline-block;
  width: 10px;
  height: 10px;
  border-radius: 50%;
  margin-right: 10px;
}

.alive {
  background-color: lightgreen;
}

.dead {
  background-color: lightcoral;
}

.unknown {
  background-color: lightgray;
}
</style>