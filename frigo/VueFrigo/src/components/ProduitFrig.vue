<script setup>
let prod = { nom: "", qte: 0 };
</script>

<template>
  <form @submit.prevent="$emit('handlerp', prod)">
    <input type="text" v-model="prod.nom" placeholder="produit" />
    <input type="text" v-model="prod.qte" placeholder="quantité" />
    <input type="button" class="buttonPanier"/>
  </form>
</template>

<style></style>