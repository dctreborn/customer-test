<template>
  <div class="details container">
      <router-link to="/">Back</router-link>

      <h1 class="page-header">{{customer.name}}
          <span class="pull-right"><button class="btn btn-danger" v-on:click="deleteCustomer(customer.id)">Delete</button></span>
      </h1>
      
      <ul class="list-group">
          <li class="list-group-item"><span class="glyphicon glyphicon-phone" aria-hidden="true"> {{customer.phone}}</span></li>
          <li class="list-group-item"><span class="glyphicon glyphicon-envelope" aria-hidden="true"></span> {{customer.email}}</li>
      </ul>
      <ul class="list-group">
          <li class="list-group-item">{{customer.address}}</li>
          <li class="list-group-item">{{customer.address.city}}</li>
          <li class="list-group-item">{{customer.address.state}}</li>
      </ul>
  </div>
</template>

<script>
export default {
  name: 'customerdetails',
  data () {
    return {
        customer: ""
    }
  },
  methods: {
      fetchCustomer(id){
          this.$http.get('http://localhost:3000/0/' + id)
            .then(function(resp){
                this.customer = resp.body;
                console.log(resp.body);
            });
      },
      deleteCustomer(id){
          console.log("you deleted " + id);
        //   add delete route when using SQL or mongo
          this.$http.delete('http://localhost:3000/0/' + id)
            .then(function(resp){
                this.$router.push({path: '/', query:{alert: 'Customer Deleted'}});
            });
      }
  },
  created: function(){
      this.fetchCustomer(this.$route.params.id);
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

</style>
