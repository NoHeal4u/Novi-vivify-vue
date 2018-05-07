<template>
  <div class="container mt-4">
    <div class="row">
      <div class="col">
        <ContactList :contacts="contacts" />
      </div>
      <div class="col-8">
        <ContactDetails :contact="routeContact" />
      </div>
    </div>
  </div>
</template>

<script>
import axios from 'axios'

import ContactList from '../components/ContactList.vue'
import ContactDetails from '../components/ContactDetails.vue'

export default {
  components: {
    ContactList,
    ContactDetails
  },

  created(){
    this.getContact()
  },

  data() {
    return {
      // contacts: [
      //   { id: 1, name: 'John Doe', email: 'johndoe@example.com', number: '555-12345' },
      //   { id: 2, name: 'Pera Peric', email: 'peraperic@example.com', number: '555-54321' },
      //   { id: 3, name: 'Nenad Vujicic', email: 'nenad.v@example.com', number: '555-67890' }
      // ]

      contacts: []
    }
  },
  computed: {
    routeContact() {
      return this.contacts.find(contact => contact.id == this.$route.params.id)
    }
  },

  methods : {
    getContact(){
      axios.get('https://api.randomuser.me/')
        .then((response) =>{
          let contact = {}
          contact.id = response.data.results[0].id.name
          contact.name = response.data.results[0].name.first
          contact.email = response.data.results[0].email
          contact.number = response.data.results[0].cell

          this.contacts.push(contact)
        })

        .catch((error) => {
          console.log(error)
        })

        axios.defaults.baseURL = 'http://jsonplaceholder.typicode.com/'

        axios.post('posts',{
          body: {firstName: 'Aleksandra'}
        }).then((response) =>{
          console.log('Success', response)
        }).catch((error) => {
          console.log('Error', error)
        })
    }
  }
}
</script>
