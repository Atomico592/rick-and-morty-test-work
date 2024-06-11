<template>
<div v-if="totalPage > 1">
      <button @click="changePage(page)" v-for="page in totalPage">{{ page }}</button>
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

</style>