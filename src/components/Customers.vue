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
  methods: {
    fetchCustomers(){
      this.$http.get('https://jsonplaceholder.typicode.com/users')
      .then(function(resp){
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
