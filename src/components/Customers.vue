<template>
  <div class="customers container">
      <h1 class="page-header">Manage Customers</h1>
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
  method: {
    fetchCustomers(){
      this.$http.get('http://slimapp/api/customers')
      .then(function(resp){
        console.log(resp.body);
      });
    }
  },
  created: function(){
    this.fetchCustomers(); //issue at this line, why?
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

</style>
