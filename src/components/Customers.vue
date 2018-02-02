<template>
  <div class="customers container">
      <h1 class="page-header">Manage Customers</h1>
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
          <tr v-for="customer in customers">
            <td>{{customer.name}}</td>
            <td>{{customer.username}}</td>
            <td>{{customer.email}}</td>          -->
            <td></td>
          </tr>
        </tbody>
      </table>
  </div>
</template>

<script>
export default {
  name: 'customers',
  data () {
    return {
      customers: []
    }
  },
  methods: {
    fetchCustomers(){
      this.$http.get('http://localhost:3000/0')
      .then(function(resp){
        this.customers = resp.body;
        console.log(resp.body);
      });
    }
  },
  created: function(){
    this.fetchCustomers();
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

</style>
