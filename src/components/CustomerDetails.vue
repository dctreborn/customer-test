<template>
  <div class="details container">
      <h1 class="page-header">{{customer.name}}</h1>
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
