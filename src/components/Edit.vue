<template>
  <div class="edit container">
    <h1 class="page-header">Edit Persons</h1>
    <form @submit.prevent="updatePerson">
        <div class="well">
            <h4>Person Info</h4>
            <div class="form-group">
                <label>First Name</label>
                <input type="text" class="form-control" placeholder="First Name" v-model="person.first_name">
            </div>
            <div class="form-group">
                <label>Last Name</label>
                <input type="text" class="form-control" placeholder="Last Name" v-model="person.last_name">
            </div>
            <div class="form-group">
                <label>Email</label>
                <input type="text" class="form-control" placeholder="Email" v-model="person.email">
            </div>
        </div>
        <div class="well">
            <h4>Person Location</h4>
            <div class="form-group">
                <label>Phone</label>
                <input type="text" class="form-control" placeholder="Phone" v-model="person.phone">
            </div>
            <div class="form-group">
                <label>City</label>
                <input type="text" class="form-control" placeholder="City" v-model="person.city">
            </div>
        </div>
        <button type="submit" class="btn btn-primary">Submit</button>
    </form>
  </div>
</template>

<script>
import axios from 'axios'

export default {
  name: 'edit',
  data () {
    return {
      person:{}
    }
  },
  methods:{
     async fetchPerson(id){
          const res= await axios.get(`http://localhost:3000/persons/`+id)
        this.person = res.data
      },
    async  updatePerson(){
          try {
               if(!this.person.first_name || !this.person.last_name || !this.person.email){
                   alert('please fill in all required fields')
               }else{
                   let updPerson = {
                       first_name:this.person.first_name,
                       last_name:this.person.last_name,
                       email:this.person.email,
                       phone:this.person.phone,
                       city:this.person.city,
                   }
                   await axios.put("http://localhost:3000/persons/"+this.$route.params.id,updPerson)
                   this.$router.push({path:'/', query: {alert: 'Person Updated'}});
            //   e.preventDefault();
          }
          } catch (error) {
              console.log(error)
          }
         
        //   e.preventDefault();
      }
  },
  created: function(){
      this.fetchPerson(this.$route.params.id)
  }
}
</script>

<style scoped>

</style>
