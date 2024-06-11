<template>
<div class="filter">
  <input v-model="filters.name" placeholder="Name"  class="inputs"/>
  <select v-model="filters.status" class="inputs">
    <option value="">All</option>
    <option value="alive">Alive</option>
    <option value="dead">Dead</option>
    <option value="unknown">Unknown</option>
  </select>
  <button @click="filterHandler" class="btn">Send</button>
</div>
</template>


<script>
export default {
  props: {
    filters: {
      type: Object,
      required: true,
    }
  },
  emits: ['apply-filters'],
  methods: {
    filterHandler() {
      this.$emit("apply-filters");
    }
  }
}

</script>


<style scoped>
.filter {
  padding-bottom: 25px;
}
.inputs {
  margin-right: 15px;
  padding: 15px 120px 15px 15px;
  border-radius: 8px;
  border: 1px solid #cccccc;
}
.btn {
  padding: 20px;
  border-radius: 10px;
  background-color:  rgb(39, 43, 51);
  border: 1px solid #ccc;
  color: white;
  font-weight: bold;
  cursor: pointer;
}
.btn:hover {
  background-color: darkslategrey;
}
</style>