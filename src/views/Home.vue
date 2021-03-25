<template>
  <div class="home">
    <h1>{{ message }}</h1>
    <h3>Create a Contact</h3>
    <p>
      first name:
      <input type="text" v-model="newContactFirstName" />
    </p>
    <p>
      last name:
      <input type="text" v-model="newContactLastName" />
      </p>
    <p>
      email:
      <input type="text" v-model="newContactEmail" />
    </p>
    <p>
      phone number:
      <input type="text" v-model="newContactPhoneNumber" />
    </p>
    <p>
      image url:
      <input type="text" v-model="newContactImage" />
    </p>
    <button v-on:click="contactsCreate">Create new Contact</button>


    <div v-for="contact in contacts">
     <p> {{ contact.first_name }} </p>
     <hr>
    </div>
    
  </div>
</template>

<style>
</style>

<script>
import axios from "axios";

export default {
  data: function () {
    return {
      message: "Welcome to Contacts App!",
      contacts: [],
    };
  },
  created: function () {
    this.contactsIndex();
  },
  methods: {
    contactsIndex: function () {
      console.log("in contacts index");
      axios.get("http://localhost:3000/api/contacts").then((response) => {
        console.log(response.data);
        this.contacts = response.data;
      });
    },
  },
};
</script>