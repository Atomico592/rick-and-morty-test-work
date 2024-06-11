<template>
<div v-if="totalPage > 1">
      <button @click="changePage(page)" v-for="page in totalPage" class="btn">{{ page }}</button>
</div>
</template>

<script>

  export default {
    props : {
      totalPage: {
        type: Number,
        required: true
      },
      currentPage : {
        type: Number,
        required: true
      }
     },
    emits: ['page-changed'],
    methods : {
      changePage(page) {
        this.$emit("page-changed", page);
      }
    }
  };

</script>

<style scoped>
.btn {
  padding: 8px;
  margin-right: 3px;
  border-radius: 8px;
  background-color:  rgb(39, 43, 51);
  border: 1px solid #ccc;
  color: white;
  font-weight: bold;
}
.btn:hover {
  background-color: darkslategrey;
}
</style>