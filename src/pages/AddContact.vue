<template>
  <div>Add Contact

<link rel="stylesheet" href="https://maxcdn.bootstrapcdn.com/bootstrap/4.0.0-beta.2/css/bootstrap.min.css" integrity="sha384-PsH8R72JQ3SOdhVi3uxftmaW6Vc51MKb0q5P2rRUpPvrszuE4W1povHYgTpBfshb" crossorigin="anonymous"> 
<link rel="stylesheet" href="https://maxcdn.bootstrapcdn.com/font-awesome/4.7.0/css/font-awesome.min.css">

<form @submit.prevent="addContact">
  <div class="form-group row">
    <label for="text" class="col-4 col-form-label">First name</label> 
    <div class="col-8">
      <div class="input-group">
        <div class="input-group-addon">
          <i class="fa fa-address-card"></i>
        </div> 
        <input v-model = "newContact.first_name" class="form-control here" type="text">
      </div>
    </div>
  </div>
  <div class="form-group row">
    <label for="text1" class="col-4 col-form-label">Last name</label> 
    <div class="col-8">
      <input v-model = "newContact.last_name" class="form-control here" type="text">
    </div>
  </div>
  <div class="form-group row">
    <label for="text2" class="col-4 col-form-label">Email</label> 
    <div class="col-8">
      <input v-model = "newContact.email" class="form-control here" type="text">
    </div>
  </div>
  <div class="form-group row">
    <label for="text3" class="col-4 col-form-label">Number</label> 
    <div class="col-8">
      <input v-model = "newContact.number" class="form-control here" type="text">
    </div>
  </div> 
  <div class="form-group row">
    <div class="offset-4 col-8">
      <button name="submit" type="submit" class="btn btn-primary">Submit</button>
    </div>
  </div>
</form>

  </div>
</template>

<script>
import { contacts } from '../services/ContactsService'

export default {

	data() {

  	return { newContact:{
  		 first_name: '',
  		 last_name: '',
  		 email: '',
  		 number: '',
  		
  	}



  }

},
	methods : {
  // 	addContact(){
  // 		contacts.add(this.newContact)
  //   		.then((response)=>{
  //   			this.$router.push('/contacts')
  //   			console.log(this.contacts)
  //   		}).catch((error)=>{
  //   			console.log(error)
  //   		})

  // 		}

 	// },


  addContact(){
          if(this.$route.params.id)
          {
            contacts.edit(this.$route.params.id, this.newContact)
           this.$router.push('/contacts')
          }
          else
          {
            contacts.add(this.newContact)
            this.$router.push('/contacts')
          }
      }
    },

 	created(){
 		 if(this.$route.params.id){
        contacts.get(this.$route.params.id)
        .then((response) => {
            this.newContact=response.data
        }).catch((error) => {
            console.log(error)
        })
      }
 	}


}
</script>

<!-- 
"first_name": "string",
  "last_name": "string",
  "email": "string",
  "number": "string",
  "id": 0
 -->