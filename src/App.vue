<template>
    <main>
        <!-- <Add_item @ajouter_liste="onInput" /> -->
         <Watchers @users="watchers_data"/>
    </main>
</template>

<script setup>
import Add_item from "@/components/Add_item.vue";
import Watchers from "./components/Watchers.vue";
import { ref } from "vue";
const users_data = ref([]);

const watchers_data = (event) => {
    users_data.value.push(event)
} 

</script>

<style scoped>


</style>


 