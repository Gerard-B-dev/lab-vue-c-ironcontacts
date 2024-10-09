<!-- src/App.vue -->
<template>
  <div id="app">
    <h1>Contact List</h1>
    <button @click="addRandomContact">Add Random Contact</button>
    <button @click="sortByName">Sort by Name</button>
    <button @click="sortByPopularity">Sort by Popularity</button>
    <table>
      <thead>
        <tr>
          <th>Picture</th>
          <th>Name</th>
          <th>Popularity</th>
          <th>Won an Oscar</th>
          <th>Won an Emmy</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="contact in contacts" :key="contact.id">
          <td>
            <img :src="contact.pictureUrl" :alt="contact.name" width="50" />
          </td>
          <td>{{ contact.name }}</td>
          <td>{{ contact.popularity.toFixed(2) }}</td>
          <td>
            <span v-if="contact.wonOscar">🏆</span>
          </td>
          <td>
            <span v-if="contact.wonEmmy">🏆</span>
          </td>
        </tr>
      </tbody>
    </table>
  </div>
</template>

<script setup>
import { ref } from 'vue';
import contactsData from './contacts.json';

// Crear una referencia reactiva que contenga los primeros 5 contactos
const contacts = ref(contactsData.slice(0, 5));
const remainingContacts = ref(contactsData.slice(5)); // Contactos restantes

// Función para agregar un contacto aleatorio
function addRandomContact() {
  if (remainingContacts.value.length > 0) {
    const randomIndex = Math.floor(Math.random() * remainingContacts.value.length);
    const randomContact = remainingContacts.value[randomIndex];
    
    contacts.value.push(randomContact); // Agregar contacto aleatorio
    remainingContacts.value.splice(randomIndex, 1); // Eliminar el contacto de la lista de restantes
  } else {
    alert('No more contacts to add!');
  }
}

// Función para ordenar contactos por nombre
function sortByName() {
  contacts.value.sort((a, b) => a.name.localeCompare(b.name));
}

// Función para ordenar contactos por popularidad
function sortByPopularity() {
  contacts.value.sort((a, b) => b.popularity - a.popularity);
}
</script>

<style scoped>
#app {
  font-family: Arial, sans-serif;
  margin: 20px;
}

table {
  width: 100%;
  border-collapse: collapse;
}

thead {
  background-color: #f2f2f2;
}

th, td {
  padding: 12px;
  text-align: left;
  border-bottom: 1px solid #ddd;
}

img {
  border-radius: 50%;
}

button {
  margin-right: 10px;
  margin-bottom: 20px;
  padding: 10px 15px;
  font-size: 16px;
  background-color: #007bff;
  color: white;
  border: none;
  border-radius: 5px;
  cursor: pointer;
}

button:hover {
  background-color: #0056b3;
}
</style>

