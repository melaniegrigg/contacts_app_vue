<template>
  <div class="home">
    <h1>{{ message }}</h1>
    <p> Add a new contact</p>
    <p>First Name:<input v-model="newFirstName" type="text"></p>
    <p>Last Name:<input v-model="newLastName" type="text"></p>
    <p>Email:<input v-model="newEmail" type="text"></p>
    <p>Phone Number:<input v-model="newPhoneNumber" type="text"></p>
      <button v-on:click="addContact"> Add!</button>

    <div v-for="contact in contacts">
      <p> First Name: {{contact.first_name}}</p>
      <p> Last Name: {{contact.last_name}}</p>
      <p> Email: {{contact.email}}</p>
      <p> Phone Number: {{contact.phone_number}}</p>
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
      message: "Welcome to Thunderdome!",
      contacts: [],
      newFirstName: "",
      newLastName: "",
      newEmail: "",
      newPhoneNumber: "",
    };
  },
  created: function () {
    this.indexContacts();
  },
  methods: {
    indexContacts: function () {
      console.log("im getting contacts meow");
      console.log("really though... is it working? What did i break");

      axios.get("/api/contacts/").then((response) => {
        console.log("contacts index", response);
        this.contacts = response.data;
      });
    },
    addContact: function () {
      console.log("addddding...adddding and.....");

      var params = {
        first_name: this.newFirstName,
        last_name: this.newLastName,
        email: this.newEmail,
        phone_number: this.newPhoneNumber,
      };

      axios.post("/api/contacts/", params).then((response) => {
        console.log(response.data);
        this.contacts.push(response.data);
      });
    },
  },
};
</script>