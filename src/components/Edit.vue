<template>
  	<div class="edit container">
  		<h1 class="page-header">Edit Customer</h1>
      <Alert v-if="alert" v-bind:message="alert" />
  		<form v-on:submit="updateCustomer">
  			<div class="well">
  				<h4>Customer Info</h4>
  				<div class="form-group">
  					<label>First Name</label>
  					<input type="text" class="form-control" placeholder="First Name" v-model="customer.firstname">
  				</div>
  				<div class="form-group">
  					<label>Last Name</label>
  					<input type="text" class="form-control" placeholder="Last Name" v-model="customer.lastname">
  				</div>
  				<div class="form-group">
  					<label>Email</label>
  					<input type="text" class="form-control" placeholder="Email" v-model="customer.email">
  				</div>
  			</div>
  			<button type="submit" class="btn btn-primary">Submit</button>
  		</form>
  	</div>
</template>

<script>
import Alert from './Alert'
export default {
  name: 'Edit',
  data () {
    return {
    	customer: {},
      alert: ''
    }
  },
  methods: {
    getCustomerById(id){
      this.$http.get('http://localhost:3000/customers?id=' + id)
          .then(function(response){
            this.customer = response.body;
      });
    },
  	updateCustomer(e){
  		if(!this.customer.firstname || !this.customer.lastname || !this.customer.email){
  			this.alert = 'Please fill in all required fields';
  		} else {
  			let updCustomer = {
          id: this.customer.id,
  				firstname: this.customer.firstname,
  				lastname: this.customer.lastname,
  				email: this.customer.email
  			}

  			this.$http.put('http://localhost:3000/customers', updCustomer)
  				.then(function(response){
  					this.$router.push({path: '/', query: {alert: 'Customer Updated'}});
  				});
  			e.preventDefault();
  		}
  		e.preventDefault();
  	}
  },
  created: function(){
    this.getCustomerById(this.$route.params.id);
  },
  components: {
    Alert
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

</style>