<template>
    <!-- {{ users }} -->
    <main>
        <div class="item-search">
            <input type="text" v-model="input_data.input" placeholder="Recherche...">
            <select v-model="input_data.filter">
                <option disabled value="">Filtre par defaut</option>
                <option>Nom</option>
                <option>Pseudo</option>
                <option>Email</option>
                <option>Adresse</option>
                <option>Site Web</option>
            </select>
        </div>
        <table border="1">
            <thead>
                <th>Nom</th>
                <th>Pseudo</th>
                <th>email</th>
                <th>adresse</th>
                <th>Site web</th>
            </thead>
            <tbody v-for="(user, id) in users" :key="id">
               <td>{{ user.name }}</td>
               <td>{{ user.username }}</td>
               <td>{{ user.email }}</td>
               <td>
                    {{ user.address.street}},{{ user.address.city}} {{ user.address.zipcode}}
               </td>
               <td> {{ user.website}} </td>
            </tbody>
        </table>
        <div class="item-bouton">
            <button class="reinitialiser" @click="reinitialiserFilter">Réinitialiser le filtre</button>
            <button class="stop" @click="stopFilter">Arrêter le filtre</button>
        </div>
    </main>
</template>

<script setup>
import {ref,reactive ,watch} from "vue";
const users = ref([]);
const input_data = reactive({
    input: '',
    filter: ''
});
const unWatch = watch(input_data, (value) => {
    fetch("https://jsonplaceholder.typicode.com/users")
        .then((Response) => Response.json() )
        .then( (json) => {
            users.value = json.filter((data) => {
                if (value.filter === "Nom") {
                    return data.name.toLowerCase().includes(value.input.toLowerCase());
                }else if(value.filter === "Pseudo") {
                    return data.username.toLowerCase().includes(value.input.toLowerCase());
                }else if(value.filter === "Email") {
                    return data.email.toLowerCase().includes(value.input.toLowerCase());
                }else if(value.filter === "Adresse") {
                    return data.address.toLowerCase().includes(value.input.toLowerCase());
                }else if(value.filter === "Site Web") {
                    return data.website.toLowerCase().includes(value.input.toLowerCase());
                }else{
                    return data.name.toLowerCase().includes(value.input.toLowerCase());
                }
            })
        })
    },{immediate:true});
const stopFilter = () => {
    unWatch();
}
const reinitialiserFilter = () => {
    location.reload();
}
</script>

<style scoped>
main{
  display: flex;
  flex-direction: column;
  place-items: center;
}
.item-search > input{
    height: 35px;
    width: 400px;
    margin-bottom: 12px;
    padding-left: 5px
}
.item-search > select{
    height: 35px;
    background-color: gray;
    color: white;
}
.item-search{
    display: flex;
}
th{
    width: 500px;
}
.item-bouton > *{
    margin-inline: 10px ;
}
.stop{
    margin-top: 20px;
    padding: 15px;
    background-color: rgb(228, 131, 3);
    color: white;
}
.reinitialiser{
    margin-top: 20px;
    padding: 15px;
    background-color: rgb(56, 115, 225);
    color: white;
}
</style>
