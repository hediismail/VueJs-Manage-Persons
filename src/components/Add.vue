<template>
  <div class="add container">
    <Alert v-if='alert' v-bind:message='alert' />
    <h1 class="page-header">Add Persons</h1>
    <form @submit.prevent="addPerson">
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
import Alert from './Alert'

export default {
  name: 'add',
  data () {
    return {
      person:{},
      alert: ''
    }
  },
  methods:{
    async  addPerson(){
          try {
               if(!this.person.first_name || !this.person.last_name || !this.person.email){
                   this.alert = 'please fill in all required fields'
               }else{
                   let newPerson = {
                       first_name:this.person.first_name,
                       last_name:this.person.last_name,
                       email:this.person.email,
                       phone:this.person.phone,
                       city:this.person.city,
                   }
                   await axios.post("http://localhost:3000/persons",newPerson)
                   this.$router.push({path:'/', query: {alert: 'Person Added'}});
            //   e.preventDefault();
          }
          } catch (error) {
              console.log(error)
          }
         
        //   e.preventDefault();
      }
  },
  components:{
    Alert
  }
}
</script>

<style scoped>

</style>
