<template>
  <div class="about container">
      <h1 class="page-header">Add Customer</h1>
      <form v-on:submit="addCustomer">
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
export default {
  name: 'add',
  data () {
    return {
        customer: {}
    }
  },
  methods: {
      addCustomer(e){
          e.preventDefault();         
          console.log("submitted"); 
          let c = this.customer;

          if(!c.name || !c.username || !c.email){
              console.log('please fill in all required fields');
          } else {
              let newCustomer = {
                  name: c.name,
                  username: c.username,
                  phone: c.phone,
                  email: c.email,
                  address: c.address,
                  city: c.city,
                  state: c.state
              }
            this.$http.post('http://localhost:3000/0', newCustomer)
                .then(function(resp){
                    this.$router.push({path: "/", query: {alert: 'Customer Added'}});
                });
          }          
      }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

</style>
