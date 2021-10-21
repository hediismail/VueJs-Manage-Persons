<template>
  <div class="Details container">
    <router-link to="/">Back</router-link>
    <h1 class="page-header">{{person.first_name}} {{person.last_name}}
      <span class="pull-right">
        <router-link class="btn btn-primary" v-bind:to="'/edit/'+person.id">Edit</router-link>
        <button class="btn btn-danger" v-on:click='deletePerson(person.id)'>Delete</button></span>
    </h1>
    <ul class="list-group">
      <li class="list-group-item"><span class="glyphicon glyphicon-phone" aria-hidden="true"></span>{{person.phone}}</li>
      <li class="list-group-item"><span class="glyphicon glyphicon-envelope" aria-hidden="true"></span>{{person.email}}</li>
    </ul>
    <ul class="list-group">
      <li class="list-group-item">{{person.city}}</li>
    </ul>
  </div>
</template>

<script>
import axios from 'axios'
export default {
  name: 'persondetails',
  data () {
    return {
      person: ''
    }
  },
  methods: {
   async fetchPerson(id) {
      try {
        const res= await axios.get(`http://localhost:3000/persons/`+id)
        this.person = res.data
      } catch (err){
      console.error(err)
     }
    },
    async deletePerson(id){
      try {
      await axios.delete(`http://localhost:3000/persons/`+id)
      this.$router.push({path: '/', query: {alert: 'Person Deleted'}})
      } catch (err){
      console.error(err)
     }
    }
  },
  created: function(){
    this.fetchPerson(this.$route.params.id)
  }
}
</script>

<style scoped>

</style>
