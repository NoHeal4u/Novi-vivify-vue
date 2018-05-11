<template>
  <div>
  Contacts

<div class="card" style="width: 18rem;" v-for="(contact, index) in contacts">
 
  <div class="card bg-secondary text-white">
    <h5 class="card-title">First Name:{{ contact.first_name }}</h5>
    <p class="card-text">Last Name:{{ contact.last_name }}</p>
    <p class="card-text">Email:{{ contact.email }}</p>
    <p class="card-text">Number:{{ contact.number }}</p>
    <p class="card-text">idTEst:{{ contact.id }}</p>
    <button v-on:click="deleteContact(contact.id , index)" class="btn btn-primary">DELETE CONTACT</button>
   <router-link class="btn btn-primary" :to="{ name: 'edit', params: { id: contact.id } }">EDIT CONTACT</router-link>
    
    
  </div>
</div>

  

  </div>
</template>

<script>


import { contacts } from '../services/ContactsService'

  export default {

    created(){
        contacts.getAll()
        .then((response)=>{
          this.contacts = response.data
          console.log(this.contacts)
        }).catch((error)=>{
          console.log(error)
        })
      },

    data() {

      return {

        contacts: []
        
        
      }
    },

    methods : {

    deleteContact(id, index) {

      contacts.delete(id)
      .then((response) =>{
        this.contacts.splice(index, 1)
      })
    },

    editContact(id){
      this.$router.push('/edit-contact')  
    }

  }

    

  }
</script>
  
<style>

</style>