<template>
  <div class="persons container">
    <Alert v-if="alert" v-bind:message="alert" />
    <h1 class="page-header">Manage Persons</h1>
    <table class="table table-striped">
      <thead>
        <tr>
          <th>First Name</th>
          <th>Last Name</th>
          <th>Email</th>
          <th></th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="person in persons" :key="person.id">
          <td>{{person.first_name}}</td>
          <td>{{person.last_name}}</td>
          <td>{{person.email}}</td>
          <td><router-link class="btn btn-default" v-bind:to="'/person/'+person.id">View</router-link></td>
        </tr>
      </tbody>
    </table>
  </div>
</template>

<script>

import axios from "axios"
import Alert from "./Alert";

export default {
  name: 'persons',
  data () {
    return {
      persons: [],
      alert: ''
    }
  },
  methods:{
    async fetchPersons(){
      try {
        const res= await axios.get(`http://localhost:3000/persons`)
        this.persons = res.data
      } catch (err){
      console.error(err)
     }
    }
  },
  created: function(){
    if(this.$route.query.alert){
      this.alert = this.$route.query.alert
    }
      this.fetchPersons();
  },
  // updated: function(){
  //     this.fetchPersons();
  // },
  components: {
    Alert
  }
}
</script>

<style scoped>

</style>
