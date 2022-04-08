<script>

import contacts from "./contacts.json";

export default {
  data() {
    return {

    hiddenContacts: contacts.slice(5),
    visibleContacts: contacts.slice(0, 5)

    }
  },
  methods: {

    addRandomContact() {

    const index = Math.floor(Math.random() * this.hiddenContacts.length);
  
    this.visibleContacts.push(this.hiddenContacts[index]);
     
    this.hiddenContacts.splice(index, 1);
    }
  },
  computed: {
    filterByName: () => {
     if (this.contacts) {
    		return this.contacts.slice(0).sort((a, b) => a.name < b.name ? this.contacts : -this.contacts )
     	} else {
    		return this.contacts
      }
    }
  }

}

</script>

<template>
  <div id="app">
    <h1>SinguContacts</h1>
    <button @click="addRandomContact">Add Random Contact</button>
    <button @click="filterByName">Sort by name</button>
    <button @click="byPopularity">Sort by popularity</button>
      <table>
  <thead>
    <tr>
      <th>Pincture</th>
      <th>Name</th>
      <th>Popularity</th>
      <th>Won Oscar</th>
      <th>Won Emmy</th>
    </tr>
  </thead>
  <tbody>
    <tr v-for="contact in visibleContacts" :key="contact.id">
      <td><img style="width: 100px" :src="contact.pictureUrl" alt=""></td>
      <td>{{ contact.name }}</td>
      <td>{{ contact.popularity.toFixed(2) }}</td>
      <td>
        <img 
        v-if="contact.wonOscar"
        src="https://img.icons8.com/external-flaticons-lineal-color-flat-icons/30/000000/external-oscar-award-video-production-flaticons-lineal-color-flat-icons.pnghttps://img.icons8.com/external-flaticons-lineal-color-flat-icons/50/000000/external-oscar-award-video-production-flaticons-lineal-color-flat-icons.png"
        />
      </td>
      <td>
        <img
        v-if="contact.wonEmmy"
        src="https://img.icons8.com/external-justicon-flat-justicon/50/000000/external-trophy-reward-and-badges-justicon-flat-justicon-2.png"
        />
      </td>
    </tr>
  </tbody>
</table>
  </div>
</template>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
