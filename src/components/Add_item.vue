<template>
    <input type="text" v-model="input_item" placeholder="Ajouter une liste..." @keyup.enter="ajouter_liste">
    <button @click="ajouter_liste">Ajouter</button>
</template>

<script setup>
import { ref } from 'vue';
const emit = defineEmits(["ajouter_liste"]);
const input_item = ref('');
const ajouter_liste = () => {
    emit("ajouter_liste", input_item.value);
    input_item.value = "";
}
</script>

<style scoped>
input 
{
    padding: 12px 24px;
}
button 
{
    width: 100px;
    height: 44px;
    background-color: rgb(14, 85, 156);
    color: white;
}
</style>