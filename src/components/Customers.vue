<template>
  <div class="customers container">
      <Alert v-if="alert" v-bind:message="alert"></Alert>
      <h1 class="page-header">Manage Customers</h1>
      <input class="form-control" placeholder="Enter Name" v-model="filterInput">
      <hr>
      <table class="table table-striped">
        <thead>
          <tr>
            <th>Name</th>
            <th>Username</th>
            <th>Email</th>
            <th></th>
          </tr>
        </thead>
        <tbody>
          <tr v-for="customer in filterBy(customers, filterInput)">
            <td>{{customer.name}}</td>
            <td>{{customer.username}}</td>
            <td>{{customer.email}}</td>
            <td><router-link class="btn btn-default" v-bind:to="'/customer/' + customer.id">View</router-link></td>
          </tr>
        </tbody>
      </table>
  </div>
</template>

<script>
import Alert from './Alert';

export default {
  name: 'customers',
  data () {
    return {
      customers: [],
      alert: '',
      filterInput:''
    }
  },
  methods: {
    fetchCustomers(){
      this.$http.get('http://localhost:3000/0')
      .then(function(resp){
        this.customers = resp.body;
        console.log(resp.body);
      });
    },
    filterBy(list, value){
      value = value.charAt(0).toUpperCase() + value.slice(1);
      return list.filter(function (customer) {
        return customer.name.indexOf(value) > -1;
      });
    }
  },
  created: function(){
    let query = this.$route.query.alert;
    if(query){
      this.alert = query
    }
    this.fetchCustomers();
  },
  updated: function(){
    this.fetchCustomers();
  },
  components: {
    Alert
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

</style>
