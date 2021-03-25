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
     <img v-bind:src="contact.image" />
     <hr />
    </div>
    
  </div>
</template>

<style>
img {
  width: 250px;
}
</style>

<script>
import axios from "axios";

export default {
  data: function () {
    return {
      message: "Welcome to Contacts App!",
      contacts: [],
      newContactFirstName: "",
      newContactLastName: "",
      newContactEmail: "",
      newContactPhoneNumber: "",
      newContactImage: "",
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
    contactsCreate: function () {
      console.log("contacts create..");
      // make a post request to the api
      console.log(this.newContactFirstName);
      console.log(this.newContactLastName);

      var params = {
        first_name: this.newContactFirstName,
        last_name: this.newContactLastName,
        email: this.newContactEmail,
        phone_number: this.newContactPhoneNumber,
      };
    },
  },
};
</script>