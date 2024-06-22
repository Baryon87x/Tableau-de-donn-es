<template>
    <main>
        <Add_item @ajouter_liste="onInput" />
        <ul v-for="(item, index) in liste" :key="index">
            <div class="todo">
                <li>{{ item.titre }}</li>
                <button @click="supprimer_item(item)">Supprimer</button>
            </div>
            
        </ul>
    </main>
</template>

<script setup>
import Add_item from "@/components/Add_item.vue";
import { ref } from "vue";

const liste = ref([]);
let id = 0;
const onInput = (input) => {
    liste.value.push({id:id++, titre: input});
}

const supprimer_item = (item) => {
    liste.value = liste.value.filter((element) => element.id != item.id );
}
</script>

<style scoped>

ul
{
    padding: 0;
}
.todo 
{
    width: 309px;
    background-color: rgba(240, 248, 255, 0.404);
    display: flex;
    justify-content: space-between;
    list-style-type: none;
    padding-left: 5px;
}
.todo button
{
    background-color: rgba(228, 11, 11, 0.953);
    color: white;
}

</style>


 