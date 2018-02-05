<template>
  <div class="edit container">
      <Alert v-if="alert" v-bind:message="alert"></Alert>

      <h1 class="page-header">Edit Customer</h1>
      <form v-on:submit="updateCustomer">
          <div class="well">
            <h4>Customer Info</h4>
            <div class="form-group">
                <label>Name</label>
                <input type="text" class="form-control" placeholder="Name" v-model="customer.name">
            </div>
            <div class="form-group">
                <label>Username</label>
                <input type="text" class="form-control" placeholder="Username" v-model="customer.username">
            </div>
          </div>

          <div class="well">
            <h4>Customer Contact</h4>
            <div class="form-group">
                <label>Email</label>
                <input type="text" class="form-control" placeholder="Email" v-model="customer.email">
            </div>
            <div class="form-group">
                <label>Phone</label>
                <input type="text" class="form-control" placeholder="Phone" v-model="customer.phone">
            </div>
          </div>

          <div class="well">
            <h4>Customer Location</h4>
            <div class="form-group">
                <label>Address</label>
                <input type="text" class="form-control" placeholder="Address" v-model="customer.address">
            </div>
            <div class="form-group">
                <label>City</label>
                <input type="text" class="form-control" placeholder="City" v-model="customer.city">
            </div>
            <div class="form-group">
                <label>State</label>
                <input type="text" class="form-control" placeholder="State" v-model="customer.state">
            </div>
          </div>
          <button type="submit" class="btn btn-primary">Submit</button>
      </form>
  </div>
</template>

<script>
   import Alert from './Alert.vue'
export default {
  name: 'add',
  data () {
    return {
        customer: {},
        alert: ''
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
      updateCustomer(e){
          e.preventDefault();         
          console.log("submitted"); 
          let c = this.customer;

          if(!c.name || !c.username || !c.email){
              this.alert = 'Please fill in all required fields';
          } else {
              let updateCustomer = {
                  name: c.name,
                  username: c.username,
                  phone: c.phone,
                  email: c.email,
                  address: c.address,
                  city: c.city,
                  state: c.state
              }
            // add update route here
            this.$http.put('http://localhost:3000/0/' + this.$route.params.id, updateCustomer)
                .then(function(resp){
                    this.$router.push({path: "/", query: {alert: 'Customer Updated'}});
                });
          }          
      }
  },
  created: function () {
      this.fetchCustomer(this.$route.params.id);
  },
  components: {
      Alert
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

</style>
