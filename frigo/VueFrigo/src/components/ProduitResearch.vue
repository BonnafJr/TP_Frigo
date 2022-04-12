<script setup>
let motcle = "";
</script>

<template>
  <form @submit.prevent="$emit('handlerr', motcle)">
    <input type="text" v-model="motcle" placeholder="rechercher" />
    <input type="submit" />
  </form>
</template>

<style></style>